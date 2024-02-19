---
tags:
  - "#legacy"
  - "#code"
package: com.cwh.xboss.tasks.data
submodule: cgslib
module: cgs
---
This holds a [[Class Player Profile]]. 
Contains [[User Data]], [[Game Session]] information and  [[Player Game Play Information]].

# Fields
## Constants
- bunch of constants with the tag names of values, probably to put write them in an xml, because why would they separate concerns?
- `int playerId` - the [[Player|player's]] id.
- `String clientAccount` - #what is this supposed to be for?
## Attributes
- #field/playerId  - [[Player Identity]]  
- `String clientAccount` - References a client's [[Account]], although it is not clear #what a client is in this context. Is it an [[Affiliate]] through which the player connects? is it the [[Player]]? 
- `String accountName`
- `String accountId`
- [[Money]] `balDep`
	- presumably the [[Deposit]] [[Balance]]
- [[Money]] `balWith` 
	- presumably the [[Withdrawable]] [[Balance]]
- [[Money]] `balPlay`
	- presumably the [[Playable]] [[Balance]]
- [[Money]] `balPend`
	- a kind of [[Balance]] which I haven't found yet. Could be pending? or #what 
- `int numSessions` 
	- presumably the number of [[Game Session]] or [[Visit]]
	- so the system must track the number of player sessions #business/process 
- `double aveDuration`
	- the average duration of a visit/session
	- so the system must track duration of visit/session #business/process 
- [[Money]] `aveSpent` 
	- the average amount the user spent per game session/visit ? #what 
	- the system must track average spent #business/process 
	- This is not really a problem, since it can be generated upon player request
		- but depending on how many users require it, it might be the case that a new table is needed to store the updated average. An event would be triggered every time a user's average changes to insert data in this table.
- `String mostPlayedGame`
	- This will require tracking how much a user plays a game and how often. #business/process 
- `String firstName` 
- `String lastName`
- `String gameName`
- `String profileName`
- [[Money]] `totalBet`
	- The total amount of money the player bet in general? #business/process  #what 
- [[Money]] `returnToPlayer`
	- I'm assuming it's how much the player got back from what he bet. 
- [[Money]] `aveBet`
	- The average amount the user bet? #business/process #what 
- [[Money]] `netWinLoss` 
	- how much the player lost? #what 
	- Somehow related to [[NetWin]]
- `BigDecimal handsPlayed` 
	- total number of [[Hand|hands]] played? #what is a hand? Does it apply to all games?
- `BigDecimal betsPlayed`
	- total number of bets placed? #what 
- `int gameId`
	- I assume there's a profile per game per player
- `int profileId` the profile's id. 
	- #why have a different profile id? why not just use playerId and gameId as composite key?
- 