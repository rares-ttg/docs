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
Other information comes in the form of a [[PlayerProfileObj]] and includes [[Game Play Information]]:
	- [[NetWin]] - this is a [[NetWinInfo]] class. 
	-  [[Class Player Profile]] class 

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


