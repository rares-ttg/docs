This is an account associated with a user. Its relation to [[Account]] is still unknown.

Fields:
- userId (self-explanatory)
- acctId
	- this account's id
- acctName
- balance
- playableBalance
	- how much the user can play
	- Should this be even a thing? Does it make business sense? #why?
- withdrawableBalance
	- how much the user can withdraw (d'oh)
- minWithdrawableBalance
	- a minimum, but #why?
- pendingBalance
	- ummm...dafuq? #what

A conceptual field is `accountBalance`. There is a getter that basically sums balance, playable balance and withdrawable balance. 
Another is `totalWithdrawable`, which is `balance + withdrawableBalance`. 

