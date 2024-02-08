It seems to be referenced as `bonusPlanInfo`  in other classes. It describes bonuses that can be offered through the app. Both money and free games can be offered as bonuses. It seems to somehow overlap with awards. 

- bonusPlanInfoId
- name
- bonusType
- bonusCode
- bonusTypeDesc
- bonusAmount
- minDeposit
- maxDeposit
- maxAccumulatedBonus
- awardFixedAmount
- awardPercentage
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
- Eligibility
	- inclAffs: List(Integer)
		- I assume this is a list of ids of affiliates included in the bonusPlan
	- inclAffiliateList: List([[Affiliate]])
		- I assume this is a list of affiliates included
		- but what's the difference between this and inclAffs?
	- incAccts List(Integer)
		- I assume this is a list of ids of included accounts
	- inclAccountList: List(Account)
		- same as above
		- why is that one integer, but this one is Account?
	- exclAccountList: List(Account)
	- exclCountries List(String)
		- I assume this is a list of excluded countries
	- inclCountryList: List(Country)
		- I assume this is a list of countries to whom the bonus plan applies. 
		- why is this a list of Country, while for exclusion Strings are used?
	- inclDeptTypeIds: List(String)
		- i assume this is a list of the type of deposits(?) that are allowed to access the bonusPlan
	- inclDepositTypeList: List([[Deposit Type]])
		- I assume this is a list of the types of depostis 
	- inclGames: List (Integer)
		- I assume this is a list of game ids which are supposed to be given for free as part of the bonus
	- exclBonusPlan
		- I assume that...nothing. I have no clue
	- 
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
- modifiedByGid
- playable
- withdrawable
- 

lsdId=it's providerId of external Game provider for EGI


| Acr | name |
| ---- | ---- |
| PFF | Play For Fun |
| PFM | Play For Money |
| LPJ | Linked Progressive Jackpot |
| EGI | External Game Integration |
| PJ  | Progressive Jackpot |
| MPJ | Multi Progressive Jackpot |


