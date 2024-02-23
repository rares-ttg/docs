---
tags:
  - business/operations
---

# CGSLib

The following are from cgs lib, the `com.cwh` packages. I assume they have to do with the common wallet. 

## Common Wallet
### Create Banner

see `com.cwh.xboss.tasks.affcomp.AddBannerTask`. It creates the banner, it does not assign it.

### My Account

`com.cwh.xboss.tasks.clientWeb.myAccount`
#### Change email
#### Change Password

#### Edit Account Limit

A player can change the deposit limit

#### Verify Account

The player can verify his account by entering the verification code. 

#### View [[Loyalty]] points [[Transaction|transactions]] 

Allows the player to view their loyalty points transactions. 
#### Redeem bonus points

The player can redeem their bonus points

#### [[Parlay]] [[Replay]]
`ParlayReplaySummaryTask`

I have no clue. I assume it is a negotiation process for games that seem dubious to the casino.

#### View personal details

In an odd twist, the class called `PersonalDetailsTask` does NOT allow users to change their personal details. It is part of an #why  called [[SNG]] Project.
#### Disable account

`PlayerAccountDisableTask`
It allows the user to obviously, disable the account. In "My Account" page, the player should have a Disable Account button.
It does not seem to be used

#### View Account Summary

`PlayerAccountSummaryTask` 
I assume it allows a user to view transactions on one financial account.

#### View [[All In]] Summary

This class, `PlayerAllInSummaryTask`, does not seem to be used. It is supposed to show a report with a Player's remaining Poker all-ins.
The reason it is no longer is use is probably because there are several Poker games.

#### View Bank Details

This is not in use. `PlayerBankDetailsTask`. It allows a user to view Bank Details.

#### Change Address

This is not in use, apparently. `PlayerChangeAddressTask`.

#### View [[Game Transaction]] Summary

This allows the player to view the transactions per game. `PlayerGameTransactionSummaryTask`.

#### View Game Replay Summary

Class `PlayerHandReplaySummaryTask`. The player can view [[Replay|replays]] of previous games. 


#### View [[Promotions]] Summary

`PlayerMyPromotionsTask`.  Does not seem to be used. Although the class is not used, the functionality might be implemented somewhere else.... because reasons. Allows players to view their promotions. #what promotions are is not known yet
#### View [[Class Player Profile|Profile]] Summary

`PlayerProfileSummaryTask` This generates a player profile report. The information included: Profile name from [[GameProfile]], [[Game Group]]  name . But the select shown in the class only looks for group name "Poker" and "Tournaments". 
Other information comes in the form of a [[PlayerProfileObj]] and includes [[Player Game Play Information]]:
	- [[NetWin]] - this is a [[NetWinInfo]] class. 
	-  [[Class Player Profile]] class 
	- 

### [[Compensation Package]]
#### Add [[Compensation Package]] to an Affiliate

`com.cwh.xboss.tasks.affcomp.AddRemoveCompPkgTask`

#### Remove [[Compensation Package]]

`com.cwh.xboss.tasks.affcomp.AddRemoveCompPkgTask`

#### Create [[Compensation Package]]

`com.cwh.xboss.tasks.affcomp.CreateCompPkgTask`

#### View [[Compensation Package]]

Will retrieve the details of  a Compensation Package specified by the user
`com.cwh.xboss.tasks.affcomp.ViewCompPkgTask`

#### Assign [[Compensation Package]] to an [[Affiliate]]

#### Retrieve [[Compensation Package]] usage

#### View [[Compensation Scheme]] Details

`com.cwh.xboss.tasks.affcomp.ViewCompSchTask`

Allows the user to view the details of a [[Compensation Scheme]]

### Affiliates

#### Affiliate add broker

`com.cwh.xboss.tasks.clientWeb.affiliate.AffAddBrokerTask` - But seems not to be used

An affiliate can add a new broker

#### Affiliate edit broker

`com.cwh.xboss.tasks.clientWeb.affiliate.AffEditBroker` - But seems not to be used

An affiliate can edit an existing broker
#### Search Affiliates

`com.cwh.xboss.tasks.affcomp.AffListSearchTask` and, for some reason also `com.cwh.xboss.tasks.affcomp.AffListTask`

Search for all affiliate information for a hierarchy of affiliates that the user has #permission to view. It has a flag to determine whether to include inactive affiliates 

#### Pay [[Affiliate]] 

Decreases the amount earned balance and increases the amount paid balance of an account type belonging to an Affiliate. The amount of the payment must be zero or greater. #why couldn't it be both pay and get paid? is it because affiliates do not make payments towards ttgs?

#### View [[Affiliate Account]]

#### Adjust [[Affiliate Acount]] 

`com.cwh.xboss.tasks.affcomp.AdjustAffAccountTask`

Adjusts the amount paid and amount earned balances of an affiliate's account. 

#### [[Affiliate Account]] Report

`com.cwh.xboss.tasks.affcomp.AffAccReptTask`


### Use [[Banner]]

`com.cwh.xboss.tasks.affcomp.BannerUseTask`

Creates a banner [[Affiliate]] which contains a tracking code that can be used to track players registrations and transactions

### Create [[Compensation Scheme]]

`com.cwh.xboss.tasks.affcomp.CreateCompSchTask`


### Immediate [[Reconciliation]]

`com.cwh.xboss.tasks.affcomp.ReconcileNowTask`

A user with #permission can force the reconciliation of a [[Compensation Scheme]] for and [[Affiliate]] to a date.

### Set compensation Periond

`com.cwh.xboss.tasks.affcomp.SetCompensationPeriodTask`

Sets the [[Compensation Period]] for a scheme

### Get Earnings by Day Report



`com.cwh.xboss.tasks.affcomp.ViewAffAccountTask`

View all account balances for all [[AccountType|account types]] 

### Add [[Marketing Campaign]]

`com.cwh.xboss.tasks.affcomp.AddMarketingCampaignTask`


##  com.chartwelltechnology.cyberboss.bonus.framework.command


### Add/Edit Bonus

BonusManager handles bonus related operations. In this case, the BonusManager calls [[BonusAddConnector]] method `setBonus` which does some weird stuff. 

### List BonusPlan

### Get Casino Properties

Returns the minimum deposit amount, the daily maximum deposit amount, the weekly and monthly maximum [[Deposit]] amount as configured in [[Configurations#casino.server.Configuration#Bonus]] 

### Search

#### Search account

Class `com.chartwelltechnology.cyberboss.bonus.communicate.AccountConnector.getAllAccount(SearchAccountRequest req)` does the work. It is invoked from  `BonusManager`. Makes a select on #table/Account for #field/accId #field/accName and `accDescription`. Creates a Vector of `AccountBean` which is set on the request object passed as parameter. Why not have a response object and set it there?
#### Search Affiliate

`BonusManager` calls `AffConnector.getAllAff(SearchAffRequest)`.  `AffConnector` makes a select over #table/Affiliate for #field/affId  and #field/affName where the affId is not in `select affiliateId from` #table/Broker . This will return all affiliates that are not [[Broker]]s. 
#### Search Bonus Plan

Searches bonus plans  from specific affiliates. 
##### Inputs
These are attributes in `SearchBonusPlanReq`
- `startValue`
- `numOfCode`
- `maxV=numOfCode+startValue`
- `bonusType`
- `String planName`
- `int[] numOfGameID`
- #field/affId 
- #field/accId 
##### Operations

1. `BonusManager` calls `BonusEditorConnector.searchBonusPlan(BonusRequest)`. 
	1. In turn, this makes a select on #table/BonusPlan where `bonusPlanName` and `affId` are inputs. Results are put in a Vector of `BonusPlanBean`s. 
	2. It then makes another select from #table/Game_Profile where #field/affId #field/gameId and #field/accId are given
		1. This is not an easy process. It does this in a complicated set of #fml while loops, making several requests to #table/Game_Profile first by #field/affId and if there are results, makes another select by #field/affId and #field/gameId and if there are any results does a select for #field/affId #field/gameId #field/accId . 
		2. If the first gameId in `numOfGameId` is 0 then it makes a select on #table/Game_Profile where #field/gameId is left open. Otherwise, it makes a for loop over `numOfGameID` and calls, IN THE LOOP, the database for each gameId, only to determine whether there are games for that Id or not. 
		3. If there are no games for that Id, then it gets the affiliate name, it makes it uppercase, then also gets game description and account name,  only to print an error message. #fml/db-hell Affiliate name, game description and account name are retrieved via db calls. It then calls break to exit the for loop. 
	3. Starts validating the entered `startValue` and `numCode` . Why do it here? what was the point of the previous db calls if these two values are invalid?
		1. Validation means doing a `select count(*)`  on #table/codedBonusRange #data/validation where `minBonusCode<=startValue<=maxBonusCode or minBonusCode<=maxValue<=maxBonusCode or (startValue<minBonusCode and maxV>maxBonusCode)` 
2. Results are put on the request
#### Search Games

Calls `BonusManager` which then calls `GameConnector.getGames(SearchGamesRequest)`
##### Input

None. `SearchGamesRequest` is just used to hold the results.
##### Operations

1. fetch from db #field/gameId and `gameDescription` for games in #table/Game_Group with `groupname in (SLOTS, VIDEOPOKER,TABLE,BINGO)`
2. Results are put in a Vector of `GameBean`  which is then put on the request.


## com.chartwelltechnology.cyberboss.flagAndAlerts.framework.command

This package has to do with  [[Alert]]s . Much like all classes in `com.chartwelltechnology.cyberboss.**.command`, the method call sequence is 
`*Cmd`->`*Manager`->`*Connector`, the latter doing all the heavy lifting. 
### Configure Alert Criteria

This creates [[AlertCriteria]]. The method called is `AlertCriteriaConnector.setOrGetCriteria(CfgCriteriaReq)`. Why would you get or insert an object in the same method is beyond comprehension #fml/db-hell . 

### Get Alert Criteria
