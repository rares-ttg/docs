---
tags:
  - "#code"
  - "#legacy"
class: NetWin
package: com.cwh.xboss.tasks.data
module: cgs
submodule: cgslib
---
This holds information about [[NetWin]]. 
## Fields

### Constants

XML Tag names are the only ones, apart from the class name which had to be added because...reasons. 
### Attributes
- `Vector gameObjects`
- [[Money]] `totalHandle`
- `String` #field/accId
- `boolean inclBonus`
	- should [[Bonus]] be included or not?
- `int playerId`
	- the [[Player Identity]]
- `int affId`
	- the affiliate's id, but is not used
## Methods

#### Constructor

The constructor...calls a stored procedure (!!?!??!). Yup. #fml #dbproc/proc_getPlayerNetwinByGameHideMinorHands 