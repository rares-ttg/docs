An [[Affiliate]] has a [[GameProfile]] for an [[Account]]

# Games

A game should have a description. It also has a [[Game Group]] 
# Bonus

A bonus plan is a specification of the criteria of awarding a bonus, the value of the bonus, its expiration day and how long it is available. Information about the bonus plan is stored in #table/BonusPlan . An awarded bonus is written in #table/AwardedBonus . Not all bonuses are playable. They can become playable if some conditions are met. A playble bonus is also a withdrawable bonus. Awarded bonuses can also be pending. So a player can be awarded a bonus, but the bonus can be in pending state for pendingDaysRemaining. 

A Bonus Award can be in the following [[Bonus Award State|states]]:
- pending(1)
- playable(2)
- spent playable(3)
- playable met (4)
- spent playable met (5)
- withdrawable (6)
- spent withdrawable (7)
- reversed (8)
- expired (9)
- stopped (10)

How does a bonus award move from one state to another? 

## Bonus Types

There are several kinds of bonus types, as listed in `com.ttg.platform.core.domain.BonusType`. However, only FREE_GAMES_ADHOC is used (in [[CIP]]). The others are there just for decoration. 

| id | Constant name | Trigger | Award Type |
| ---- | ---- | ---- | ---- |
| -1 | BONUS_CHOICE_ALL | All | null |
| 0 | DEPOSIT_BONUS_TYPE | Deposit | Fixed |
| 1 | DEPOSIT_FIXED_BONUS_TYPE | Deposit | Fixed |
| 2 | DEPOSIT_PERCENT | Deposit | Percentage |
| 3 | REGISTRATION_BONUS_TYPE | Registration | Fixed |
| 4 | CODE_BONUS_TYPE | Coded | Fixed |
| 5 | FREE_GAMES_ADHOC | AdHoc | FreeGames |
| 6 | FREE_GAMES_QUALIFIED_PLAYERS | QualifiedPlayers | FreeGames |
| 7 | FREE_GAMES_DEPOSIT | Deposit | FreeGames |
| 8 | FREE_GAMES_CODED | Coded | FreeGames |
| -2 | FREE_GAMES_ALL | AllFreeGames | FreeGames |

### Events 

updateBonusBalance event

 
## Bonus Award 

### Award Events

#### Registration

A bonus is awarded by default when the user [[Registration|registers]] in the application. See `com.chartwelltechnology.cyberboss.bonus.bobject.PendingBonus`.  This seems to be the default option and it makes sense from a marketing perspective, however, it should not be hard coded, since it could be disabled in some cases. Instead, registration should emit an event and a bonus processor should listen to it. #business/event 
##### Scenarios
###### Scenario 1
1. User registers without specifying 
	1. the plan
2. Input:
	1. #field/accId 
	2. #field/affId 
	3. 
3. Registers through SDK, Download, processRegistration, Poker or Add Player
###### Scenario 2 

1. User registers **under a specific plan** 
	1. Input:
		1. #field/playerId 
		2. #field/accId 
		3. #field/affId 
		4. #field/bonusPlanId
		5. #field/bonusType 
			1. This method is always called with bonusType=3, i.e. [[Coded Bonus]]. 
2. Registers through SDK, Download, processRegistration, Poker or Add Player
###### Scenario 3

1. User registers under **a specific plan and currency name**
	1. Input
		1. #field/playerId 
		2. #field/curName  
		3. #field/affId 
		4. #field/bonusPlanId
2. Registers through SDK, Download, processRegistration, Poker or Add Player
##### Mechanism

###### Scenario 1
This is handled in `PendingBonus.notifyRegistration(int playerId,int accId, int affId)` which calls `PendingBonus.createRegistrationBonus(playerId,accId,affId)` #fml/db-hell/query-spam

1. If the player has a [[Broker]] and #configuration/brokerTriggerBonus  is false, then the player does not receive a bonus.
2. verify if the player qualifies for the plan
	1. call `PendingBonus.searchBonusPlan()` with #field/playerId #field/accId #field/affId 
		1. calls `BonusPlanConnector.getBonusPlan(playerId,accountId, amount=0,bonusType=BonusPlanBean.TYPE_REGISTRATION)`
			1. for the given #field/affId **and its ancestors** find all **enabled** plans which may qualify
				1. select fom #table/BonusPlan  
					1. where bonus plan is enabled and the current time is between the plan's start/end dates.
					2. bonus plan #field/affId  is the same as the one provided
				2. Eliminate bonus plans where the deposit limits have been met or the profiles don't match to games
					1. It is a call to `BonusPlanConnector.getBonusPlan(playerId,accId, Money amount, affId, bonusType, bonusPlanId, gameProfiles,)`
					2. select from #table/BonusPlan  the enabled bonus plans that have not expired (current date and time is between the plan's start/end date time) and that are associated to the affiliate and the account given as input.
					3. for deposit type bonus plans (fixed amount or percentage) check if maximum bumber of bonuses (deposits) or accumulated limit has been reached for this player
						1. Translation: 
- [ ] finish understanding the Bonus mechanism. See `PendingBonus`
3. Insert new AwardedBonus with status=pending.
4. Notify player
5. receive bonus if playable immediately



### Transaction

BonusAwardTrans marks a transaction when a bonus is awarded. BonusAwardTransType marks the type of transactions. Each class has a corresponding table: #table/BonusAwardTrans and #table/BonusAwardTransType 

##### Type 

The types of bonus award transactions are
1. withdrawable
2. playable
3. metric
4. freegame
5. freegamepending
6. wager

This taxonomy does not make much sense. A free game is the object of a bonus, not a mode of interaction (withdrawable, playable). Same with metric, which I don't know what is yet.

## Bonus Plan

A BonusPlan applies to some games, not all. There is a Many2Many relation between Games and BonusPlan. See `BonusPlanInfoGame`. 
A check must be made to see if the player qualifies for the bonus plan. 
Can be **disabled**. 

There are four types of bonus plans:
1. Deposits
	1. Fixed `BonusPlanBean.TYPE_FIXED=1`
	2. Percent `BonusPlanBean.TYPE_PERCENT=0`
2. Registration `BonusPlanBean.TYPE_REGISTRATION=2`
3. Coded `BonusPlanBean.TYPE_CODED=3`
### Playable bonus

When a bet is made the gaming system notifies the bonus system to apply the bet against one or more pending bonuses for the player. The calculation is done in `com.chartwelltechnology.cyberboss.bonus.javaBean.A2Bean`. 


