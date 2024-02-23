---
tags:
  - module
---
# Overview

Location relative to root `cgs` project folder: `webapps/cip`.
It is a jersey REST service. The endpoints are in package `com.ttg.cip.rest.service`. They all inherit from `BaseService` which is in the same package, which also inherits `com.ttg.rest.service.CoreService` (outside `cip` package). `CoreService` has a reference to an ibatis SqlSessionManager which it gets from a guice `Injector` used in a totally absurd way. 

# Paths
## /affiliate

### /login

This is handled in `AffiliateLoginService`, but through some `reflection gymnastics ` the work ends up being done in `AffiliateAuthenticationCommand.execute(AuthenticationModel)`.  `AuthenticationModel` is an interface implemented by `AffiliateLoginRequest`. The latter is actually sent to the `execute` method. It only holds the username and password in plain/text. The `execute` method invokes `AffiliateAuthenticationCommand.authenticate(model)`. This is the workhorse. 

#### Request

A request can be a regular request, or a `T24` request, whatever that is 

##### Headers
The headers must contain the [[Affiliate|affiliate's]] username (`Affiliate-Id`) and the affiliate's password (`Affiliate-Login`).  If it is a `T24` request, then the headers have a `T24-` prefix.

#### Process

The credentials, as they should've been called, are then sent to an `AffiliateAuthenticationCommand`, which is in `ttglib` and checks the credentials, somehow. Returns a token if it exists, or a new token otherwise.

- [ ] [CIP]Really look into how the credentials are checked.
#### Response

There are regular responses, and `T24` responses, corresponding to the same kind of requests. The response headers contain the token, the expiration date, and whether it is a new token or not. So, the headers are
- `Affiliate-Granted-Token`
- `Affiliate-Granted-Token-Expiry`
- `Affiliate-New-Token-Granted`, values yes/no.
with `T24-` prefix for `T24` requests

- [ ] Find out what `T24`  is #cip
#### Dependencies

Depends on [[com.ttg.security.command]] in [[ttglib]]

#### Process

`AffiliateAuthenticationCommand.execute(AuthenticationModel)` gets the username and password from the model.  It then uses `EncryptPassword.getHashString` to generate a `SHA` hash (not `SHA-2`).  The username is the #field/lsdId which is then used in conjunction with #field/siteId to get the corresponding #field/affId). It then checks if the (hashed) password matches the one from the db #table/AffiliatePassword . 

Generates a token. which is basically a `UUID.randomUUID()` concatenated with a random number between ten million and one hundred million (-1).  The token is then inserted in the db by calling #dbproc/update_officializeAffiliateSecurityToken . The procedure also determines the token expiry date. So, yes, the expiry date is set in a stored procedure. 

If something goes wrong, it returns an `AffiliateAuthenticationStatus.INVALID_LOGIN`
## /freegame/eligibility

Handled by `FreeGameEligibilityService`. 

Checks whether the affiliate is eligible for a free game, using the affiliate's authentication details. 

### Headers

Same as before, it's either 

- `Affiliate-Granted-Token`
- `Affiliate-Granted-Token-Expiry`
- `Affiliate-New-Token-Granted`, values yes/no.
Or 
- `T24-Affiliate-Granted-Token`
- `T24-Affiliate-Granted-Token-Expiry`
- `T24-Affiliate-New-Token-Granted`, values yes/no.
### Dependencies

Also on [[ttglib]] via [[com.ttg.security.command]].

### Process

1. Extracts authentication information from request headers into an `AffiliateAuthenticationRequestInfo`
2. authenticates affiliate `FreeGameEligibilityService.authenticateAffiliate(AffiliateAuthenticationRequestInfo)`
	1. Creates a validation Service: `new AffiliateTokenValidationService()`
		1. The constructor calls `startSessions()` where
			1. Checks if there's an active session `org.ttg.platform.core.session.ThreadSessionController.isSessionStarted()`
				1. `ThreadSessionController` has a `ThreadLocal<Session>` attribute, where `Session` is an interface `com.ttg.platform.core.session` (same package). There is a single implementation of `Session`,  `com.ttg.cip.session.ThreadSession`
					1. ThreadSession contains a list of `ThreadEventNotification` objects
					2. and a `com.ttg.security.session.AffiliateLoginSession`. 
						1. This has an #field/affId , the security token, the expiryTime, and a #field/lsdId
				2. `ThreadSessionController.isStarted()` only checks if the `ThreadLocal<Session> localSession` attribute is null or if the encapsulated `Session` object.
			2. If not, then it creates a new `ThreadSession`: `ThreadSessionController.startSession(new ThreadSession())`
			3. calls local method `AffiliateTokenValidationService.startSQLSession()`  to initialize the MyBatis SQL Session.
				1. If the session is already started, throw `RuntimeException`
				2. otherwise call `SqlSessionManager.startManagedSession(ExecutorType.REUSE,false)`
	2.  It then calls `AffiliateAuthReqUtil.authenticateAffiliate(AffiliateAuthenticationRequestInfo, IAffiliateTokenValidationService, AffiliateAuthenticationCommand)`
		1. To be sure, there is `IAffIliateTokenValidationService` AND `AffiliateTokenValidationService`. The latter is an interface implemented by the former
		2. `authenticateAffiliate()` then calls `IAffiliateTokenValidationService.validateToken` with parameters 
			1. `AffiliateAuthenticationRequestInfo` which has a bunch of `public final` attributes initialized in the constructor.
				1. `affiliate_Id`(username), `affiliate_Login`(password),`affiliate_Token` as well as their `t24` counterparts
				2. #field/lsdId
				3. `boolean isT24Header`
				4. `String token` which I assume is the affiliate's token
				5. `String loginAuth` 
				6. But `token,loginAuth and lsdId` are not passed as constructor parameters, but are assigned the values received as parameters thus:
					1. #field/lsdId = #field/affId  or `t24` equivalent if the first is null
					2. `loginAuth` is the `affiliate_Login` or `t24_affiliate_Login` if it is a `t24` request
					3. `token` = `affiliate_Token` or `t24_affiliate_Token` if it is a `t24` request;
			2. `validateToken` creates an `AffiliateTokenValidation` and invokes `validateToken(lsdId,token)` on it. 
			3. if the token is expired, it `renewToken()`
				1. calls `SecurityService.renewToken()` 
3. Constructs a `FreeGameEligibilityRequest` by calling `FreeGameEligibilityService.constructFreeGameEligibilityRequest(AffiliateAuthentication)`
	1. This creates a new instance of `FreeGameEligibilityRequest` (only has #field/affId and #field/lsdId )
	2. it sets the request's `lsdId` from `AffiliateAuthentication`
	3. and it gets the #field/affId from `AffiliateDAO`(see [[Affiliate Identity]]) 
	4. Both are set on the `FreeGameEligibilityRequest` object that is returned to the caller
4. Then it invokes `FreeGameElligibilityCommand` via #fml/reflection
	1. in the `Command`'s execute method, it invokes via MyBatis (`FreeGameEligibilityMapper`) a gigantic select. From what I can gather, it checks whether the 
## /freeSpins

Handled by `FreeSpinsService`.
### /freeSpins/get

Contrary to its name, this is a `POST` request, because reasons. 
Input, this is in `FreeSpinGetRequest`: 
- clientAccount
- siteId
- #field/lsdId

### /freeSpins/add

Also a Post. Consumes and Produces JSON
Inputs. from `FreeSpinsAddRequest`
- clientAccount
- partnerId
- gameId
- amount
- int freeSpinValue
- String expireDate `yyyy-MM-dd hh:mm:ss`
- String promoCode
- #field/siteId 
- #field/lsdId 
- int txnId

It creates a brand new [[BonusPlan]] for the player. So #what is the difference between a [[BonusAward]] and a [[BonusPlan]]?

See `PlayerFreeGamesBonusPlanCommand.addFreeGamesBonusPlanByPlayer`
1. Takes the playerId and retrieves the [[Player]] by calling `playerDAO.getPlayerIdAndAccount(clientAccount,siteId)` . 
2. gets the [[Affiliate]] id #field/affId  from `affDAO.getAffiliateId` with #field/clientAccount and #field/siteId 
	1. if no affiliate is found, then it will use the player's #field/affId  from `player.getAffiliateId()`
3. gets a [[BonusPlan]] with [[Domain#Bonus Types|bonus type]] FREE_GAMES_ADHOC from `PlayerFreeGamesBonusPlanCommand.addFreeGamesBonusPlanByPlayer` with parameters: playerId, modifiedByGid: 0, exclCountries:null, affId, affIdSet, player: p, request)
	1. bonus plan is enabled 
	2. has priority 1. [[BonusPlanPriority]] not instantiated. 
	3. the excluded countries is set to the received parameter (which is null in this case, and in all other cases, since the method is only called once, unless it is called via reflection)
	4. the #field/bonusType  is set to 1 (`BonusType.FREE_GAMES_ADHOC.getBonusType())`
	5. the #field/bonusCode is set to `null` 
	6. the maxNumberBonus is set to 1. #what does is this supposed to mean?
	7. set the maxNumberBonus**All** to 1
	8. sets the applyCommunityMetric to 0 #what is this?
	9. sets `firstTimeDeposit` to 0.
	10. set `isForPlayerGroup` to 0 #what
	11. sets the start date to today
	12. set the expiration date to the value gotten from the request object (req.getExpiredDate)
		1. if none specified, then set it to 7 days from startDate (the value 7 is hard coded. Yes #fml/hard-code)
	13. end date and stop date ( #what is this and how is it different from expiration date) are set to the value of the expiration date.
	14. `freeGamesNumber` is set to the amount from the `FreeSpinAddRequest` object #what is this ? It is not in any other bonus plan class #fml/type-hell 
	15. the bonus amount on the other hand is set to `request.getFreeSpinValue` and divided by 100 (so it's a percentage)
	16. the bonus plan's base account is set to the id of [[Account#Player|the player's account]]. 
	17. the `comments` attribute of BonusPlan is set to `promoCode=` concatenated with the #field/promoCode from the request
	18. the bonus plan's name is set to `Free game ` concatenated with the `txnId` from the request.
	19. condition amount type is set to `BONUS_AMOUNT_TYPE_WITHDRAWABLE_NO_CONDITION`. #what does this mean?
	20. **SAVES THE BONUS PLAN**  in #table/BonusPlanInfo 
	21. gets `bonusPlanInfoId` from the saved Bonus Plan object just saved.
	22. creates a new entry for #field/bonusPlanInfoId  and #field/affId  in #table/BonusPlanInfoAffiliate 
	23. creates a new list to which it adds #field/gameId 
	24. the bonus plan's included games (`inclGames`) list is set to the list previously created.
	25. also sets the `inclConditionGames` to the same game list
	26. it then creates a new entry in #table/BonusPlanInfoIncConditionGame
	27. then another entry to #table/BonusPlanInfoExcludedCountry
	28. Calculates the [[Domain#Bonus Award]] and Awards the saved bonus plan to the Player (calls `PlayerFreeGamesBonusPlanCommand.getBonusAwardFromBonusPlan`) with parameters bonusPlan: the bonus plan just saved, bonusAwardStateId: PLAYABLE_STATE_ID, playerId: the one received, a set of #field/affId and the [[Player]] object
		1. #why send the playerId and the Player? Also, [[Bonus Award State]] are hardcoded in `BonusTagLib`, why make another constant?
		2.  The method allegedly checks to see if the player is in the [[CasinoOperator|CBUser]]'s list of affiliates and if it is not, then it does not create the bonus award. However, the method is only called once (in the case currently discussed), in a case in which this is always the case #why ? #deprecated ?
		3. The **BonusAward** object is created with the following values being set
			1. accountId=bonus plan base account Id
			2. award amount = bonus amount (which was `request.getFreeSpinValue/100`)
			3. bonusAwardStateId, bonusPlanInfoId same from bonus plan
			4. conditional balance and deposit are set to 0
			5. metric count and metric total are also set to 0
			6. the playerId and affiliate id are taken from the method parameters
			7. [[Playable]] bonus [[Balance]] , Playable [[Win]] Balance and [[Withdrawable]] Balance are set to 0
			8. the BonusAward object is returned
	29. It is then persisted in #table/BonusAward 
	30. The BonusPlan object is returned
4. Sends a GameEvent 

