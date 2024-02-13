It seems to be referenced as `bonusPlanInfo`  in other classes. It describes bonuses that can be offered through the app. Both money and free games can be offered as bonuses. It seems to somehow overlap with awards. 

- #field/bonusPlanInfoId
- name
- [[Bonus Type]]
	- bonusType
		- where are the bonusTypes declared?
		- are the types: Money, Games, both?
	- bonusTypeDesc
- #field/bonusCode
- bonusAmount
- minDeposit
- maxDeposit
- maxAccumulatedBonus
- [[BonusAward]] - not so sure it refers to BonusAward class, though
	- awardFixedAmount
	- awardPercentage
- State
	- enabled
- firstTimeDeposit:int
- isForPlayerGroup:int
- applyCommunityMetric: int
- startDate
- endDate
- createDate
- expiryDate 
	- what is the difference between endDate,stopDate and expiryDate? I assume expiryDate is the date when the bonus offer to the player expires.
- stopDate 
	- what is the difference between endDate and stopDate?
- playerGroupFileName-What is this?
- comments
- batchNumber
- [[Eligibility]]
	- [[Affiliate]]
		- inclAffs: List(Integer)
			- I assume this is a list of ids of affiliates included in the bonusPlan
		- inclAffiliateList: List([[Affiliate]])
			- I assume this is a list of affiliates included
			- but what's the difference between this and inclAffs?
	- [[Account]]
		- incAccts List(Integer)
			- I assume this is a list of ids of included accounts
		- inclAccountList: List(Account)
			- same as above
			- why is that one integer, but this one is Account?
		- exclAccountList: List(Account)
	- [[Country]]
		- exclCountries List(String)
			- I assume this is a list of excluded countries
		- inclCountryList: List(Country)
			- I assume this is a list of countries to whom the bonus plan applies. 
			- why is this a list of Country, while for exclusion Strings are used?
		- exclCountryList(Country)
			- why is this a Country, while the first one is a list of Strings?
	- [[Deposit]]
		- inclDeptTypeIds: List(String)
			- i assume this is a list of the type of deposits(?) that are allowed to access the bonusPlan
		- inclDepositTypeList: List([[Deposit Type]])
			- I assume this is a list of the types of deposits
		- exclDepositTypeList
	- [[Game]]
		- inclGames: List (Integer)
			- I assume this is a list of game ids which are supposed to be given for free as part of the bonus
		- inclConditionGameList List([[Game]])
			- what is a ConditionGame and why is it a game?
		- exclGameList: List(Game)
		- exclConditionGameList List(Game)
			- same question as beforre
	- BonusPlan
		- exclBonusPlan
			- I assume that...nothing. I have no clue
		- includedBonusPlanList(BonusPlan)
		- excludedBonusPlanList
	- [[BonusPlanPriority]]
		- bonusPlanPriorityList
			- I'm at a loss. I have no clue what this means?
	- [[PlayerGroup]]
		- playerGroupList
		- 
- Condition
	- conditionType
	- conditionExpiryDay
	- conditionAmountType
	- conditionAmountTypeDesc
	- conditionAmount
- maxNumberBonus
- maxNumberBonusAll
- priority
- #field/modifiedByGid
	- id of global user that created the Bonus Plan
- [[BonusPlanType]]
	- playable
	- withdrawable



#field/lsdId = id of external Game provider for EGI


| Acr | name |
| ---- | ---- |
| [[PFF]] | Play For Fun |
| [[PFM]] | Play For Money |
| LPJ | Linked Progressive Jackpot |
| EGI | External Game Integration |
| [[PJ]]  | Progressive Jackpot |
| [[MPJ]] | Multi Progressive Jackpot |


