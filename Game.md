A Game can be added to a [[GameSuite]].  It has a [[GameProfile]] 

# Legacy implementation
## Declarations

Game class is declared in multiple modules/packages, with some differences between them.
In [[Backoffice]] there is a single Game class. In [[CGS]] there are 10, but they might not all be used. 
So, in `cgslib` we find
- `com.chartwelltechnology.server.game`
- `com.cwh.fcs.game`
- `com.cwh.xboss.profile.model`
- `com.chartwelltechnology.cyberboss.flagAndAlerts`
- `com.cwh.lpj.model`
- `com.cwh.casino.promotion.model`
- `com.cwh.casino.promotion.service.model`
In [[CIP]] there are some other packages
- `com.ttg.platform.core.domain`
In [[Platform core]] we have
- `com.amaya.platform.core.domain`
And in [[ttg-game-event-messaging]] there's another one in
- `com.ttg.game.event.messaging.model`

These are also not entirely duplicates. Although they have a lot of fields in common, their names are different. So in one you might find `String mode` while in another `GamePJMode pjMode`. Whether the mode property refers to 
## Fields
All of them. And I mean really all of'em. From all 11 classes. The basis is the Game class from Backoffice

- #field/gameId - [[Game Identity]]
- gameName
- mode: String
	- might have something to do with pjMode
- pjMode: GamePJMode
	- found in  Game class in `com.chartwellltechnology.server.game`
- pjEnabled: boolean
	- I assume it has to do with [[Jackpot]], particularly with [[Progressive Jackpot]]
- pjWinChannelId: int
- gameIdForMPJ: int
	- not used, probably has to do with [[Mystery Jackpot]]
- groupId
	- probably links to [[Game Group]]
- groupName:
	- this one is found only in Game class in `com.chartwellltechnology.server.game`
- startGameType: int
- paramProperties
- gameStatus: int #what
- scopeId: int
	- #what is a game scope? Is it a thing?
- inCyberBossReports: int #what 
	- why is it an int and not a boolean?
- bonusMoneyAllowed: int 
- game_launchable
- isParentGame: boolean
- parentGameId
	- #what is a [[Parent Game]]?
- childGames: List (Game)
- remoteServiceUrl: string #what
- freeGameEligibilityParamList: List of FreeGameEligibilityParam 
	- Assumption: the game has a set of parameters which are supposed to be used to determine whether the game can be given away for free in some conditions.
	- I don't know yet #how the eligibility is to be determined.
- bonusGameId: String
	- #why string when gameIds are int?