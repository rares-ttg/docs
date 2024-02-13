
## Legacy 

There are several transaction classes:
- in [[CGS]] `/cgslib` - 
	- `com.chartwelltechnology.server.transaction.Transaction`
	- `com.chartwelltechnology.cyberboss.TransactionBean`
		- This seems to be used for reporting purposes and calls the previous `Transaction` class
- In [[Data Feed|Dataservice]] - `com.ttg.datafeed.model.action.Transaction` 


A transaction can have several (I say several instead of 2 because God knows what else I will find) states
1. CLOSED `com.amaya.platform.core.service.AccountingService`:
2. APPROVED Both 
3. DECLINED `com.ttg.datafeed.model.action.Transaction`
### CGS Implementation

According to `com.chartwelltechnology.server.transaction.Transaction`, a transaction can be initiated by a [[Player]], a [[CasinoOperator]] or they can be [[Game]] play transactions.

#### Fields

##### Constants

There are quite a lot of constants in this class:

- [[Transaction Type]] - It would be more appropriate to call it Transaction source.
	- `AT_TRANS_TYPE="AT"`
		- player initiated transactions. #why AT then?
	- `MT_TRANS_TYPE="MT"`
		- casino operator initiated transactions #why MT?
	- `GT_TRANS_TYPE="GT"`
		- game play transactions. #why GT and not GP?
- Status
	- `APPROVED_STATUS` = `AUTHID_APPROVED` din [[DBCommTrans]]
	- `DECLINED_STATUS` = `AUTHID_DECLINED` din [[DBCommTrans]]
- `HOUSE_ACCOUNT_ID="0"` #why Strings with integer values?
- `EXTERNAL_ACCOUNT_ID="-1"`
	- #why The funny bit about these two is that they are actually used and cannot be changed 🤮
- `FUN_ACCT_TYPE_ID=1`
- `REAL_ACCT_TYPE_ID=2`
	- These two have to do with Fun Money vs Real Money. It is related to [[PFF]] and [[PFM]] 
	- `REAL_ACCT_TYPE_ID` is not used

##### Attributes

- `int _userId`#why the underscore in front of them?
- `long _ID`
- `long _handId=0` 
	- Does it make sense to make transactions relative to hands? #what Is the concept of transaction related to that of a banking transaction or is it something internal? Or both?
- `int _transIDLink`
- 




