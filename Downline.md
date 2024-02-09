Downline has to do with [[Partner|partners]]. A downline partner is a partner that is not root, but is further down the partner hierarchy. 

Fields:
1. membership: [[Membership]]
2. #field/affId
	1. [[Affiliate]] id.
3. #field/playerId:int
4. name
5. status
6. statusName
7. directPlayerCount
	7. I assume this is the total number of players connected directly to the system
8. directDownlineCount
	1. I assume this is the total number of partners connected? #what ?
9. totalHierarchyPlayerCount
	1. I assume it is a count of all players in the partner hierarchy. See Figure.1
10. totalHierarchyBrokerCount
	1. Probably the number of all the [[Broker|brokers]] (external gaming systems from whom TTG got the game)
11. [[Balance]]
	1. totalBrokerBalance
	2. totalMemberBalance
	3. availableBalance
12. userAccount: UserAccount
13. drillDownEnabled: boolean=true
	1. I have no idea what this is about. The only reference found was in the frontend ts files. Seems to have to do with [[NetWinTab]]
14. totalRowMajorSort
	1. [[NetWinTab]] related. 
15. countryId: String
	1. whose country? Why not a damn foreign key? 


Figure 1 ![[Partner System.svg]]()