An affiliate is any external system that receives or sends games from the TTG System. Affiliates that give games to TTG can be found in #table/Broker and are called [[Broker]]s. A complete list of affiliates is in [[AffTypes]] . Partners and webmasters are all those that receive games from TTG. 

See ![[Partner System.svg]]

# Fields

1. #field/affId - the main id
2. State variables
	1. status:int
	2. active: 1
	3. state:String
3. #field/lsdId 
	1. LsdId generation #business/process
		1. an id the affiliate uses to identify himself in the system
		2. First, affiliate requests, in person, a lsdId. 
		3. Then, TTG admin [[Adding Affiliates|adds]] the affiliate with the id
		4. the affiliate's app sends requests to our app with the lsdId
4. [[Affiliation Details]]
	1. affDate - the affiliation date
	2.  affiliateType: String
		1. #why is this here, and why is it String?
	3. affiliateName
	4. affiliation: int
		1. A code comment claims that this maps to partner in table #table/partner #why
	5. special: int
6.  Contract
	1. contractStartDate
	2. contractEndDate
7. notes #table/comments
8. Hierarchy
	1. Parent
		1. parentName
		2. parentId
	2. Children
		1. numChildren
		2. descendants
	3. directPlayerCount
	4. hierarchyPlayerCount
	5. isDownline
	6. directDownlineCount
		1. See [[Downline]]
	7. hierarchyBrokerCount
9. Bonus
	1. inheritBonusPlans: int
		1. #what I assume that it is a flag that determines whether  
11. inactiveHourId: int #what? 
12. #field/modifiedByGid
	1. It is the identifier of the GlobalUser that (last) changed it.
13. #field/siteId
	1. the field siteId, though not this one in particular, is referenced in [[IncompleteHand]] , as well as [[PlayerGroup]]. So the SiteId might be something relevant since all these entities have it
14. [[Address]]
	1. city: String
	2. country: String
	3. countryId: String : #why ?
	4. zipCode: String
	5. address: String 
		1. #why another address? What can they possibly write here?
15. [[User Credentials]]
	1. userName
	2. nickName
	3. password
	4. pwdReEnter
16. [[Personal details]]
	1. firstName
	2. lastName
	3. url
	4. imgId
		1. Profile image?
17. [[Contact]]
	1.  contactInfoId: int
		1. But there are also contact details further down below.
	2. dayPhone
	3. eveningPhone
	4. tollPhone
	5. email
	6. emailSec
	7. fax - why not smoke signals?
19. External Identifiers
	1. #field/globalId
	2. #field/brokerId
	3. #field/playerId 

## State

Can be active/inactive.