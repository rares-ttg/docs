---
aliases:
  - NetWinTab
---


## NetWinTab

NetWinTab is a class which configures the visualisation configuration of NetWin for [[Affiliate]],[[Game]],[[GameSuite]],[[GameProfile]],[[GameDeviceType]],month,day, [[Player]], [[Account]], [[Country]], all of the previous, or NO_DAY(??)
Fields
- Flags (booleans)
	- viewAffiliate
	- viewGame
	- viewGameSuite
	- viewGameProfile
	- viewGameDevice
	- viewMonth
	- viewDay
	- viewPlayer
	- viewAccount
	- viewCountry
- Strings
	- netWinGroupBy
		- this is a filter, I suppose
	- netWinLabel
There are a bunch of String constants, which hold names of labels. But also a bunch of static NetWinTab class variables (not declared final). 