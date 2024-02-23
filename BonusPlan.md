There are several classes by that name. 
## BonusPlanBean

This is in `com.chartwelltechnology.cyberboss.bonus.javaBean.` 
### Fields
- `int planId`
- `planName`
- `int enable=1`
- `BigDecimal minDep` 
	- it is the minimum [[Deposit]]
- `BigDecimal maxDep`
	- maximum [[Deposit]]
- `BigDecimal maxAccuBonus`
	- presumably the maximum accumulated [[BonusPlan]]
- `int maxNumDep`
	- #what is this?
- `int type`
	- whether it is a percentage [[Bonus]] or a cash bonus
- `BigDecimal bonus=0`
- `BigDecimal playableCondition`
- `BigDecimal withdrawableCondition`
- `int pendingExpiryDays`
	- I'm assuming this is the number of days until the bonus plan expires #what
- `int playableExpiryDays` #what 
- `String fromDateTime`/`String toDateTime`
	- the dates between which the bonus plan is viable
- `String createDate`
	- date of creation
- #field/accId 
	- id of [[Account]]
- `String acctName`
	- name of [[Account]]
- `String affName`
	- the [[Affiliate]] name
	- this seems to be the same as #field/lsdId in db #why
- `int allGames` #what
- `int expired`
- `BigDecimal bonusChips` [[Chip]]
- `BigDecimal playableConditionChips`
- `BigDecimal withdrawableConditionChips`
- `int cBonusStartValue`
	- this is [[Coded Bonus]] start value. 
- `int cBonusNumOfCode`
	- [[Coded Bonus Range]] 

### Bonus Plan Info

