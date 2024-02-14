
## Legacy 

There are several transaction classes:
- in [[CGS]] `/cgslib` - 
	- `com.chartwelltechnology.server.transaction.Transaction`
	- `com.chartwelltechnology.cyberboss.TransactionBean`
		- This seems to be used for reporting purposes and calls the previous `Transaction` class
- In [[Data Feed|Dataservice]] - `com.ttg.datafeed.model.action.Transaction` 
- In 


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
	- This is the default Id of the house
- `EXTERNAL_ACCOUNT_ID="-1"`
	- Stands for check or credit card Ids
	- #why The funny bit about these two is that they are actually used and cannot be changed 🤮
	- are these actually flags? 
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
- `String _date` #why a String?
- `Money _amount`
- `Money _bonusAmount`
- `Money _withdrawableBonusAmount`
- `Money _playableBonusAmount`
- `Money _balance`
- `Money _bonusBalance`
- `Money _playBonusBalance`
- `Money _withdrawBonusBalance`
- `String _status`
- `String comments`
- `String _type` 
	- automatically a player initiated transaction
	- It is made an MT transaction manually
	- the game makes it a GT.
- `String _subType`
	- Visa, Master Card, Black Jack, Check
	- #why is there no distinction drawn between them? Visa, MasterCard, are card providers, a Check requires interaction with a bank of sorts, while BlackJack is a [[Game]]
- `String _referenceID`
	- GameID, Check#, wire# - #why no distinction? What about validation?
- `String _toAccountID` 
- `String _fromAccountID`
- `String _refAccountID = HOUSE_ACCOUNT_ID` which means it's always 0;
- `String _transactionNumber`
- `String errorCode`
- `String _errorMsg`
	- #why put these here? 


#### Methods

Apart from the usual getters and setters, there are some methods, mainly static, which return boolean that are used in some special getters :`getSDKMyAccountTransactions` , `getTransactions` all of them and  `getCommerceTransactions...`  (all methods). These are used either for reports, or for retrieving transaction details to display to the user. 