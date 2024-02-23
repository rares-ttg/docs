This might be related to `awardFixedAmount` and `awardPercentage` in [[Bonus Plan]], although it is not clear #why code duplication occurred. 
BonusAward seems to refer to a bonus that was given to a player. Bonuses can give free money or free games.  
- [  ] what is the relation between this and [[Domain#Bonus Award]]

Fields
- bonusAwardId - self-explanatory, I hope
- bonusPlanInfoId
	- this refers to the [[BonusPlan]], but it is not clear whether there are more BonusAwards for a single BonusPlan, or the relation is one to one.
- playerId - self-explanatory, refers to [[Player]]. Then again, it might not be so clear
	- This is the id of the player that was awarded the bonus (isn't it?)
- affiliateId - [[Affiliate]], I suppose
- accountId - This refers to the [[Account]]
- [[Freebie]]
	- Money - this is one kind of bonus that can be given
		- deposit - #what does this refer to? It is not the amount, since that one is below
		- awardAmount
		- playableBonusBalance
		- playableWinBalance
		- withdrawableBalance
	- [[Game]] another kind of freebie
		- freeGamesAwarded: int
			- how many games we originally given for free 
		- freeGamesRemaining: int 
			- how many games the user can still play
			- presumably, this is decremented every time the user plays another free game.
- bonusAwardStateId - refers to [[Bonus Award State]]
- awardDate
	- the date the bonus was given to the player?
- [[Metric]]  - I dunno what this is. There is also an  `applyCommunityMetric` in [[BonusPlan]]
	- metricCount
	- metricTotal
- conditionBalance
	- dafuq is this?
- conditionMultiplier:int
	