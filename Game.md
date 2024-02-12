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

- #field/gameId - [[Game Identity]]
- gameName
- mode: String
	- corresponds
- pjEnabled: boolean
	- has to do with [[Jackpot]], particularly with [[Progressive Jackpot]]
	- 