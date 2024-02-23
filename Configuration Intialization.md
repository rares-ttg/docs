---
tags:
  - legacy
  - configuration
---
Number of queries:

```math
# AMS 2
parents=31
children=857
total = (parents + children)*4
# AMS 3
parents=8
children=45+29+18+6+4+2+1+1
total = (parents + children)*4
# AMS 5
parents=30
children=61+33+32+23+15+13+12+10+10+8+8+7+7+6+5+5+5+4+4+4+3+3+3+3+2+2+2+2+1+1
total = (parents + children)*4
# AMS 7
parents = 2
children = 15 +1
total = (parents + children)*4
# AMS 11
parents=2
children=4+2
total = (parents + children)*4
# AMS 12
parents=9
children=31+17+1+2+1+9+57+6+2
total = (parents + children)*4

```
## casino.server.Configuration
This is the main configuration file from what I can gather. A WIP documentation is [[Configurations#casino.server.Configuration|here]] . In it, there is a static block which is executed when the class is loaded in memory. The following is a sequence diagram of what goes on in that mess. 

```plantuml

database Database as db
participant "com.chartwelltechnology.server\n.user.AccountTypes" as AccountTypes
Configuration -> "com.cwh.license\n.client.License": updateLicense()
activate Configuration
Configuration  ->Configuration: loadCasinoPropertiesXML("casinoProperties.xml")
Configuration -> DbConnection: pool.getConnection()
activate DbConnection
DbConnection->Configuration: dbConn=dbConnection
deactivate DbConnection
deactivate Configuration
note over Configuration
	Read Database Table for default Casino Properties
end note
Configuration -> Configuration: loadDBInfo()
activate Configuration

note over DbConnection
	yes, again
end note
Configuration ->DbConnection: pool.getConnection()
Configuration-[#red]>db: "select pname,pvalue,affId from CasinoProperties"
db-[#red]>Configuration: casino properties values
group#red while [iterate over select results]
	note right
		fillKey is the method with\n
		1200 lines of if-else conditionals
	end note
	Configuration -> Configuration: <font color="red">fillKey(pname,pvalue,propertyAffId)</font>
end 
Configuration ->Configuration: reloadUserAccounts()
activate Configuration
note right
	Loads the accounts from the database
end note
Configuration-> AccountTypes: findAccounTypeNames()
activate AccountTypes
AccountTypes-[#red]>db:"select accName From account where..."
db-[#red]>AccountTypes: account data
AccountTypes->Configuration: Vector accountnames
deactivate AccountTypes
deactivate Configuration
deactivate Configuration
|||
note over Configuration:This method reads the info\n about DB from casinoProperties.xml\n and fills up the keys

Configuration ->Configuration: loadXMLInfo()
activate Configuration
group#red for-loop [loop over the configuration for each affiliate]
	group#red for-loop [iteration over each affiliate's properties]
		Configuration -> Configuration: <font color="red">fillKey(pname,pvalue,propertyAffId)</font>
	end
end 
deactivate Configuration
|||
note over Configuration: Pre-loads skin mapping for all affiliates.\n We check if each affiliate has a custom skin\n defined in the CasinoProperties table\n if not we navigate up the hierarchy\n until we find an appropriate skin
Configuration -> Configuration: loadSkinMap()
activate Configuration
create AffHier
Configuration -> AffHier: new AffHier(Affiliate.getLicenseeID())
activate AffHier
create MiniAff
AffHier->MiniAff:new MiniAff(affId)
activate MiniAff
MiniAff->MiniAff:init()
create AffStore
MiniAff->AffStore: new AffStore()

MiniAff->AffStore: getMiniAff(this)
activate AffStore
AffStore->AffStore: findMiniAff(miniAff)
activate AffStore #green
AffStore->DbConnection: [[[pool.acquire()]]]
AffStore-[#red]>db: "select....from Affiliate join AffToRatt LO Join AffHierarchy"
db-[#red]>AffStore: Affiliate data
create AffType
AffStore->AffType: new AffType()
AffType->DbConnection: pool.getConnection()
DbConnection->AffType: DbConnection
AffType-[#red]>db: "select ... from AffType"
db-[#red]> AffType: affTypeData
AffType->AffStore: AffType object
create RattType
AffStore->RattType: new [[[RattType]]]()
activate RattType
RattType->RattType: init()
RattType->DbConnection: [[[pool.acquire()]]]
DbConnection->RattType: DbConnection
RattType-[#red]> db: select ... from Ratt
db-[#red]>RattType: [[Rule of Affiliate Transaction Tagging|Ratt]] info
RattType->AffStore
deactivate RattType

AffStore->MiniAff: MiniAff
deactivate AffStore
MiniAff-> AffHier: MiniAff
deactivate MiniAff
|||
group#red recursive call to AffHier init()	
	AffHier->AffHier: init()
	AffHier->AffStore: getAffHier(this)
	activate AffStore
	AffStore-[#red]>DbConnection: pool.getConnection()
	DbConnection-[#red]>AffStore: DbConnection
	AffStore-[#red]>db: "selectChildId from affhierarchy where parentId=?"
	db-[#red]>AffStore: affiliate children 
	group#red while [iterate over children]
		
			create AffHier
			AffStore->AffHier: new AffHier()
			activate AffHier #red
			AffHier->AffHier: <font color="red">init</font>
			AffHier->AffStore: AffHierarchy
			deactivate AffHier
		
	end
end
AffStore->AffHier: affiliate hierarchy
deactivate AffStore
AffHier->Configuration: AffHier
deactivate AffHier
Configuration->AffHier: getHierarchy()
AffHier->Configuration: Vector of MiniAff
group for-loop [iterate over hierarchy vector]
      Configuration->Configuration: load a map with affiliates,\n except common wallet affiliate
end 
group for-loop[iteration over skinURI (array constant in Configuration)]
     group while-loop [iterate over affiliates]
          Configuration->Configuration: getSkinProperty(affId,propName)
     end 
     Configuration->AffSpecificConfiguration: affSpecificConfigProps.get(affKey)
     note over Configuration: some setters are invoked\n on the AffiliateSpecificConfiguration object
end 
deactivate Configuration
|||
note over Configuration: Now we check correct Payout Levels\n It is just a bunch of ternary expressions
Configuration->Configuration: checkLevels()

```
## ConfigurationInitializer


```plantuml

ConfigurationInitializer -> GamingLogger:getGamingLogger()
activate ConfigurationInitializer
ConfigurationInitializer->Configuration: skinPaths
Configuration->ConfigurationInitializer : Set skinPaths
group while [iterate over skinPaths]
  ConfigurationInitializer -> Configuration: skinPaths.get(skinPath)
  Configuration->ConfigurationInitializer: (TreeSet)skinPathAffIds
  group while [iterate over skinPaths by affiliateId]
    ConfigurationInitializer-> Configuration: getProperty(affId,"ResCacheManager")
    Configuration->ConfigurationInitializer:ResourceCacheManager
    ConfigurationInitializer->ResourceCacheManager:loadResources(servletContext,skinResourcePath)
    activate ResourceCacheManager
    ResourceCacheManager -> ResourceCacheManager: "getResourcePathsFromContext\n(servletContext, contextPath, recursive=true)"
      group for [iterate over resource paths]
        ResourceCacheManager -> ResourceCacheObject: "new ResourceCacheObject\n(resourceName,resourcePath, servletContext)"
        ResourceCacheObject -> ResourceCacheManager: ResourceCacheObject
        
      end
      ResourceCacheManager->ConfigurationInitializer: int (number of resources added \n to the internal resourceMap)
    deactivate ResourceCacheManager
  end
end
deactivate ConfigurationInitializer

```
