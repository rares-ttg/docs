---
tags:
  - business/valueobject
---
The information is retrieved in [[Class Player Profile]] in method `getBankingInfo`. However, it is not clear how exactly this is retrieved, since the method makes a select on #table/PeriodMetaData and #table/PeriodTypes and retrieves some TABLE NAMES!?!? #why. And then, there's an iteration over the results (?!?!!?) and a select is run on table names retrieved from the previous select. 

This is how it gets the [[Withdrawable]] [[Balance]], the [[Bonus]] [[Balance]], and the [[Deposit]] [[Balance]]. #fml . It is also how it gets the [[NetWin]] information. 