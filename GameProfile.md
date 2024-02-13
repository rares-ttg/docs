Game Profiles can be activated or de-activated. When such an operation occurs, some actions need to be taken. Class [[GdkGameChangeAction]] defines the type of actions that must be performed on de/activating a Game Profile. While the class appears in [[Backoffice]], there is an interface of the same name in `com.cwh.gdk.game.ash.amazonwild.gdk.model`. So it is related to [[Ash Games]] somehow.

From this perspective, there are two kinds of games: Those that do their own processing (of #what) and those that expect the system to do it for them (auto-completion). If the game opts for autocomplete, then the game should tell the system which game request marks the end of a game round. Without this information, the system will not be able to identify the time to perform default processing. If the needs to update historical data after that, it should also specify the class definition of the updater. (Paragraph taken from comment in `com.cwh.gdk.common.pojo.GdkGameChangeAction`).
# Fields

- [[Game]]
	- gameId: - parent game's identifier
	- gameName: is this necessary? Just join the game table
- profileId- d'oh
- profileName
- [[Affiliate]]
	- #field/affId
	- affName 
		- The affiliate's name? Why not an Id?
		- does Game Profile apply only to games sent to Affiliates? #why 
- suiteId
	- Is it suiteId or #field/siteId ?
- State
	- activeint 
	- #what is this about? what depends on this?
- [[Currency]]
	- #field/curName 
	- #field/curId
- [[Account]]
	- outputAccId
- [[Linked Progressive Jackpot]]
	- lpjGameProfile: int
		- #why ? is this a flag or an id?
	- lpjDisabled: int
		- #why int? why not boolean, FFS?
- [[GameDeviceType]]
	- deviceTypeId. I'm assuming it's about the game device type
	- deviceName
- [[Chat]]
	- chatChannelIndex
- scopeId - #what ?
- #field/groupId #what 

## The Interface

In the GameProfile *interface* in `com.cwh.gdk.game.ash.amazonwild.gdk.model` there are some getters and setters that can give a bit more insight into what a GameProfile is. This might be associated to Ash Games in particular. 

Methods:
- isValidStake(Money stake)
- getMaxStake: Money
- getMinStake: Money
- getDefaultStake: Money
- getMaxWinnings: Money
- getProfileElement: jdom.Element

### Implementations

An implementation of the interface is `DefaultProfile` which appears to be configured from an XML. `DefaultProfile` is implemented by `SlotsProfile`,`ShuffleProfile`, and `AmazonWildProfile`, but only the latter seems to be implemented. 

# GameProfileSettings

This is a class in `casino.server`, so is part of the [[Casino]]
Fields:
- parametersVector which contains : minBet,maxBet,MaxStraightUpBet,MinInsideBet,MinOutsideBet.
- inputAccIds: List 
- outputAccId: int
- linkedJackpotGameProfileId: int
- linkedJackpotDisabled