Fields
- accId
	- I assume this is the id in the db
- accName
- accDescription
- [[Currency]]
	- curId
		- currency Id, presumably
	- #field/curCode
		- because curId was not enough
	- #field/curName
		- because id and code is not enough
	- currencyScale
		- this is an #why
- #field/modifiedByGid
	- the [[Global Identity]]  of whoever created the account.
- [[AccountType]]
	- defaultAccountForCurrency: boolean
		- I suppose this determines whether for a given currency this the account that should be used
		- so there can be more Accounts for the same currency
	- bankable: int
		- Shouldn't this be a boolean? I'm assuming it's just 1 or 0
## Player

The player too has an account. Several, actually.