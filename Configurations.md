# casino.server.Configuration

Now this is one hell of a #fml/if-hell . There is a 1200 lines series of if-else statements called in a double for-loop. Nevertheless, we must look over it in the hopes that it gives us some more information about the overall application structure and business logic. 


Some properties concern [[Logging]] , others configure the various servers to which the app is supposed to connect to
## Servers
- `bossserver`
- `clientserver`
- `memberserver`
- `webmasterserver`
- `registrationserver`
- `sdkserver`
- `gamesserver`
- `bankserver`
- `AlternateServerUrl` #what ???
- `casinoFlashServletUrl` 
		- I assume this is no longer used.
- `String siteIdAttr`- is this #field/siteId ? #what 
- `imageDir` #what
	- folder to upload images to
	- or folder to store images used in app? Wouldn't surprise me. 
- `soundDir` #what
		- folder for sounds
- `String userAccount[]=new String[0]` #what #why 
	- what is this array for?
- `String bottomlessAccount[]=new String[0]` #what  is this?
- `bottomlessAmount`
- `bottomlessMinimum`
- `String accounts` #what
## Casino
- siteIp
	- related to #field/siteId ?
## [[Registration]]
- `registrationCancelRedirectURL`
- `registrationBaseTemplateURL`
- `registrationCasinoURL`
- `xmlRegistrationServletURI`
- `confirmationNumber` #what 
- `registrationForm`
- `loginForm`
- `confirmationForm`
- `confirmationFeature`
## [[E-mail]]
- `mailhost`
- `mailsender`
- `webmastermailsender`
	- #what is this supposed to be? does it send just to [[Webmaster]]?
- `mailconfirmline`
	- #why line? is this supposed to be a telephone line or smth?
- `mailsubject` 
- `welcomesubj`
- `welcomemsg`
- `welcomemsgconf`
	- #why need an extra configuration? The message is right above.
- `ccrecipient`
## [[Account]] 
is it [[User Account]] instead?
- `clientAccount`
- `accountExpiry`
## [[Game Session]]
- `clientSession`
 - `baseAttributes` #what 	- 
- `regFomsPath` #what
## [[User Data]]
- `firstName`
- `lastName`
- `userName`
- `nickname`
- `displayName`
- `email`
- `password`
- `changePassword`
- `mothersMaidenName` #why is this necessary? 
- `baseAccount`			
	- I'm assuming this is the default user [[Account]]
- `boolean useCreditCard`
- `toBeContactedByEmail`
- `String regDate` - registrationDate?
- `regAffId`
- `PFFAccName` 
	- This is the name of the [[PFF]] [[Account]]? #what
- `PFRAccName`
	- the name of the [[PFR]] account? #what 
- `PFFStartId=0`
- `PFFEndId=0` - I have no clue #what this is. 
### [[Country]]
- `String country`
- `countryCode`
- `countriesExcluded`

## [[Banking]]

public static int bankDetailTxnSubType = -1;  
public static Map bankNumPmtAcctAllow = new HashMap();  

- `boolean enableBanking=false` #business/process 
	- #why isn't this enabled by default? 
	- does it have to do with [[PFF]] and [[PFR]]?
## [[Bonus]]

// Temporary Parameters for Bonus Coupons  
public static boolean couponEnableRedemption = false;  
public static int couponRegistrationBonus = 0;  

// Sleep/Counts for BonusHandlers  
private static final String EVENT_CONFIG_HANDLER = "event.config.handler";  
public static Map handlerProperties = new Hashtable();  

- `enableNewBonus=false` #business/process 
	- this has to do with [[Bonus]] but I don't know #how yet
- `boolean enableBonus=true` same as above
- `boolean overflowBonusDeposit=false`
	- #business/process  but #what ?
- `affiliatesInheritBonusPlansDefault` #business/operations 
	- #what does inheritance mean in this context?
- `boolean bonusIncludePlayable=false`
- `boolean gpBonusIncludePlayable=false`
	- both these flags are supposed to control whether playable bonuses that contribute to regular and GP bonus systems #what ?
	- has to do with [[GPBonusPlanLoader]]
- `int gpBonusPlanLoaderRestSeconds=60`
	- This is how many seconds the [[GPBonusPlanLoader]] should sleep to refresh memory #what ?
- `eventWriteBonus=false`
	- #what is this?
- `bolean` #configuration/brokerTriggerBonus  #business/operations
	- this has to do with [[Broker]] [[Bonus|bonuses]], but #what?
-  `totalRewardsLevel=0`
	- #what


### [[Deposit]]
- `String minDepositAmount = null;`
	- //Configurable deposit Amount  
- `String dailyMaxDepositAmount = null;  `
- `String weeklyMaxDepositAmount = null;  `
- `String monthlyMaxDepositAmount = null;  `
- `String depositLimitWaitingPeriodDays = null;  
- `boolean forceGameType = false;`
		- //Resume configuration   
## [[Notifications]]
- `minutesForSearchAlerts`
	- #what are search alerts?
- `Properties addProperties`
	- #what ?
- `String addProps` #what ?
	- is this necessary given the previous property?
## [[Licensing]]
- `String licenseFile="CasinoLicense.xml`
- `boolean licenseCheck=true`
## [[Visit]]
- `int visitTimeOut=4`
	- This is the default visit time of 4 hours
	- so a visit ends after 4 hrs
## Mobile(?)

- `String parentServletURL`
	- no clue #what this is
- `boolean notifyParentServlet=false`
	- #what?
- `String parentAuthenticationServletURL`
	- this is for [[Mobile Game]] to get authentication from parent site
- `boolean needParentSiteAuthentication=false`
- `boolean createNewPlayer=false`
	- #what is this supposed to mean?
- `String parentBalanceURL`
	- this is for [[Mobile Game]] to transfer chips from parent site
- `parentChipsTransferURL`
- `boolean transferChipsFromParentSite=false`
		- I assume this is a #feature/flag 
- `String communityLogin="CommunityLogin` 
			- #what is this for?
## Games
- `int casinoOrBingo=0` #what
		- shouldn't this be a boolean, if it's a flag? 
- `double startingBalance=0.0`
- `boolean checkLSD=true` #what 
- [[Bingo]] - Bingo75 and 90 stats interval  
	- `statsUpdateInterval = 60; // In terms of seconds`
### Slots
#### Configurable [[Slots]]
- `int treasureChestLevel = 0`
- `golfLevel=0`
- `int fruitBasketLevel=0`
- `int fastTrackLevel=0`
- `int wildWestLevel` 
	- #what are levels?
- `int potoGoldLevel`
- `int nationalAirLevel`
- `int jewellaryChestLevel` - yes, that's how they spelled it.
- `spaceInvasionLevel`
- `iwinLevel=0` 
- `int foytLevel=0`
- `fiveReelSlotssLevel=0` #what is this?
- `String TC`
- `String FT`
- `String WW`
- `String PG`
- `String JC`
- `String SI`
- `String GOLF`
- `String FRUIT`
- `String FOYT`
- `String IWIN`
- `String NA`
- `String TR`
- - `boolean processBingoEvent=false` #what #business/event 
- `int bingoPayoutType=1` 
	- #what does 1 mean?!?!

#### Generic Slots 
Generic Slots Test Mode  
public static boolean genericSlotsTestMode = false;  
### Poker  
public static String pokerRulesPath = "";  
public static int pokerCountdown = 30000;  
public static int pokerLobbyCache = 0;  
public static boolean pokerProtocolXML = true;  
public static boolean pokerProtocolString = false;  
public static boolean logReplay = false;  
public static boolean logFunGames = false;  
public static boolean pokerIpRestriction = false;  
public static int pokerSitNGoDelay = 0;  
## Database
- [[DbPortability]] `DBP` #what?
	- not the most portable application, so why did they even try?
	- `int potBroadcastInterval=0`
	- `int msgBroadcastLife=0`
	- `boolean winnerEmailEnabled=false`
	- `String winnerEmailSubject`
	- `String winnerEmailMsg`
	- `String defaultparlaydepositpromocode`
	-  `String parlayserver = null;  `
	- `boolean parlayEnabled = false;`
## SharedState Configuration  
- `int sharedCleanupInterval = 0;`
- `int sharedStateLife = 0;`
- `int clockEngineInterval = 0;`
	- // Com.Chartwell.clock something
  
## Xboss  

// Cyberboss  
public static int cbMainMenuForClient = 0;   // 0 - standard, 1 - for client  

public static String xbossPresentationURI = null;  
public static String xbossURI = null;  
public static String xbossTaskServletURI = null;  
public static String xbossAJAXValidationServletURI = null;  
public static boolean xbossReportByLoginAffiliate = true;  
public static boolean xbossReportByCalendar = true;  
public static boolean xbossReportByCurrencyConversion = false;  
public static String xbossWebAppName = null;  
public static String xbossServerURI = null;  
private static String siteReportingCurrency = null;  

// both xbossSearchablesURI and xbossSortablesURI should eventually be removed.  
public static String xbossSearchablesURI = null;  
public static String xbossSortablesURI = null;  
These two are not used. They seem to have been removed
### Transactions

public static int playerTransactionMaxRowQuerySize = 10000;  
public static int transactionMaxRowQuerySize = 10000;  
  
### UserInfo

public static String userinfoTaskServletURI = null;  

## Date Formats
public static String dbDateRegEx = null;  
public static String inputDateRegEx = null;  
public static String dbDatePattern = null;  
public static String inputDatePattern = null;  

## Stylesheets

//stylesheets loaded from class & folder  
public static String stylesheetsLoadClass = null;  
public static boolean stylesheetsReload = false;  
  
//stylesheets TransformerFactory system property  
public static String stylesheetsTransformerKey = null;  
public static String stylesheetsTransformerValue = null;  
### Replay stylesheets
public static String replayStylesheetTransformerValue = null;  
## EGI 

// EGI related Properties  
public static boolean egiPresent = false;  
public static String egiIntegrationService = "chartwell";  
  
public static String transactionServerURL = "";  
public static int transactionServerConnectionTimeOut = 30000;  
public static boolean enableEGIResumeCheck = false;  
## [[RNG]]
// RNG  
public static int seedSize = 0;  
public static String rngServerURL = "";  
public static int rngRange = 0;  
public static boolean isConnectToRNGServer = false;  
public static int batchLimitPercent = 0;  
  
## Batch phone games
//batch phone games  
public static boolean enableBatchPhoneGame = false;  
public static String supportedBatchPhoneGames = "";  
  
## Phone games  
public static boolean includeFunAccountForPhone = false;  
  
## Currency Rate
CurrencyRateUpdater  
public static Element currencyRateSites = null;  
public static long currencyRefreshRate = 0l;  
  
## Community 
// Community Related Variables  
public static boolean communityEnable = false;  
public static boolean communityAccess = false;  
public static int siteId = -1;  
public static String siteLicenseName = null;  
public static String siteHeader = null;  
  
public static boolean timerEnable = true;  
public static String siteExternal = null;  

## Jurisdiction 
// Jurisdiction parameters. can only be set once at startup and cannot be changed on the fly.  
public static final String siteJurisdiction; // jurisdiction: set in static initializer below  
public static final int siteBetLength; // bet-length: set in static initializer below  
public static final boolean siteAutoBet; // auto-bet: set in static initializer below  
public static final boolean siteTurboBet; // turbo-bet: set in static initializer below  
public static final String softwareRNG; // software-RNG class to use in case we are not connected to hardware-RNG: set in static initializer below  
public static final String siteClientTime; // time: set in static initializer below (either Real or Session)  
public static final boolean siteBuyFeature; // buy-feature: set in static initializer below  
private static String jurisdiction; // for fillKey  
private static int betLength; // for fillKey  
private static boolean autoBet; // for fillKey  
private static boolean turboBet; // for fillKey  
private static String rngClass; // for fillKey  
private static String clientTime; // for fillKey  
private static boolean buyFeature; // for fillKey  
  
public static boolean limitLiability = false;  
  

  
## DAOMapping  
public static HashMap daoClassMap = new HashMap();  
  
## Misc 
public static int archivedataolderthan = 0;  
public static String site = "";  
public static boolean resumeBlackjackCrossDevice = false;  

## casinoProperties.xml
  
//The time of last modification for casinoProperties.xml  
static long lastModified = 0l;  

## Session Attribute Monitor

// For the SessionAttributeMonitor, values specify num seconds.  
public static int sessionAttrTimeoutCheckInterval = 0;  
public static int sessionAttrTimeout = 0;  

## Caching

// For resource caching  
public static int resourceCacheTimeout = 0;  
public static ResourceCacheManager ResCacheMgr = new ResourceCacheManager(0);  


// Cache settings for CwhCache  
public static String cacheURL_Default = null;  
public static int cacheRetries = 5;  
public static long cacheWaitTime = 30000l;  
public static boolean cacheEnableMonitor = true;  
public static long cache_lease_RTT = 500l;        // The defined Round Trip Time for notification renewals  
public static long cache_lease_BTW = 0l;          // The defined Batch Time Window for notifications  
public static long cache_lease_DUR = 5l * 60000l; // The defined Lease Duration Interval for notification renewals  
  
## Skins

// Identify all the base URI properties that define skins.  
public static String[] skinURIs = new String[]{"CasinoSkinURI",  
        "PokerSkinURI",  
        "CyberbossSkinURI",  
        "UserinfoSkinURI",  
        "AffiliateSkinURI",  
        "CyberbanxSkinURI",  
        "RegistrationSkinURI",  
        "FUPSkinURI",  
        "ParlaySkinURI",  
        "ReplaySkinURI"};  
  
public static String CasinoSkinURI = null;  
public static String PokerSkinURI = null;  
public static String CyberbossSkinURI = null;  
public static String CyberbanxSkinURI = null;  
public static String UserinfoSkinURI = null;  
public static String AffiliateSkinURI = null;  
public static String RegistrationSkinURI = null;  
public static String FUPSkinURI = null;  
public static String ParlaySkinURI = null;  
public static String ReplaySkinURI = null;  
  
// Keys by skin path, value is the affId  
public static HashMap skinPaths = new HashMap();  
public static Set skinnedAffIds = new TreeSet();  

## Affiliates
  
private static HashMap affSpecificConfigProps = new HashMap();  
  
public static HashMap domainAffIdMap = new HashMap();  
public static String domainName = null;  

public static long affiliateIdCacheSleep = 10 * 60 * 1000;  
public static long affiliateIdCacheMaxAge = 24 * 60 * 60 * 1000;  

  
//The time of last modification for Data Base  
public static String timeStamp = "";  
  
//For refresh()  
public static boolean reloadXMLConfig = false;  

## Logging
// flag to control logging info in loadDBVendor() only once  
// to stdout  
private static boolean alreadyLogged = false;  

## Database
// ys-2005-01-28 db connection debug  
public static boolean dbconnDebug = false;  
public static int dbconnMonitorRestSec = 60;  
public static int dbconnMaxLiveTimeInSec = 120;  
// endo of ys-2005-01-28  
public static int uniqueKeysDbPoolSize = 5;  
  


## Versioning 

// Will be used to store the build version as built into the web.xml at build time.  
public static String buildVersion = "undefined";  

## User login
//unique login  
public static boolean uniqueLogin = false;  
  
## Scheduling

public static String schedulerSyncAddress = null;  
public static int schedulerSyncPort = 0;  
public static String schedulerSyncInterface = null;  
public static String schedulerAllowIdentifiers = null;  
public static String schedulerDenyIdentifiers = null;  
  
## [[Linked Progressive Jackpot|LPJ]]

public static String lpjEnabled = "false";  
public static long lpjUpdateRate = 10 * 1000;  
public static int lpjTolerance = 0;  

## [[Progressive Jackpot]]

// progressive jack related  
public static int pjUpdateTime;  
//the ttl for a pj update messag. It is by millisecond  
public static long pjMessageTTL = 5000;  
public static long pjWinMessageTTL = 120000;  
public static int pjProcessEventNumber;  
public static boolean pjUpdateCache = true;  
## [[Mystery Progressive Jackpot|MPJ]]
public static long mpjWinMessageTTL = 20000;  
//mpjupdate message will be send after this time since MPJBalanceUpdateTime started  
public static long mpjUpdateDelay_ms = 120000;  
public static long mpjUpdateInterval_ms = 5000;  
public static int newMPJConnTimeout = 30000;  

## [[SNG]] [[Reality Check]]

// 7830 SNG Reality Check  
public static boolean rcEnable = false;  
public static boolean pslEnable = false;  
public static int rcIntervalCheck = -1;   // in minutes  
public static int rcIntervalSchedule = 1; // in minutes  
public static int rcType = -1;  
public static int rcBetInactivityTime = 0;  
public static int rcLockPlayerUntilTime = 0; // in minutes  
public static int rcMsgType = 1;  
public static boolean rcAllowPlayerDisable = false; // allow player to turn off rc  
// End of 7830 SNG Reality Check  

## Time Stamping Service
// time-stamping service  
public static boolean timeStampEnabled = false;  
public static String timeStampKeystoreFileName = "xboss/casino_cms.keystore";  
public static String timeStampKeystorePassPhrase = "storepass";  
public static String timeStampKeystoreType = "pkcs12";  
public static String timeStampKeyAlias = "alias";  
public static String timeStampKeyPassword = "keypass";  
public static String timeStampCertFileName = "xboss/casino_cms.cer";  
public static String timeStampCertType = "X.509";  
public static String timeStampTsaUrl = "http://149.239.16.135/Signtrust/TSP/servlet/httpGateway.PostHandler";  
public static int timeStampTsaTimeout = 8000;  
public static String timeStampFtpUrl = "ftp://62.8.159.146";  
public static String timeStampFtpUserName = "anonymous";  
public static String timeStampFtpPassword = "tsp@chartwelltechnology.com";  
public static int timeStampFtpTimeout = 3000;  
public static String timeStampFtpWorkFolder = "chartwell";  
  
  
## Responsible Gaming 

// Responsible Gaming - CR7830  
public static String timeLimitedStatusTypes = null;  
public static int timeLimitedStatusMaxDays = 30;  
public static String genericStatusConfirmationMessage = null;  

## Address Verification Service server
// Avas server url  
public static String avasServerUrl = null;  
  
## Captcha
public static String captchaServletURL = null;  
public static boolean isCaptchaEnabled = false;  
public static String captchaIdURL = null;  

## Fop server
I don't know what this is, there might have been a module at some point, but in pom.xml the module is commented out. #deprecated 
// fopserver  
public static String fopServletURL = null;  
public static boolean fopEnabled = false;  
## Fup webapp
Same as [[#Fop server]] 
//fup webapp  
public static String fupServerURL = null;  
public static String fupEmailTemplateURL = null;  
public static int fupEmailExpireTime = 4; //in hours  

## Black List
public static boolean blacklistEnabled = false;  
public static String blacklistProviders = null;  

## Registration normalization
#what is registration normalization? 
public static String regnormalizationdeffilename = null;  
public static String regnormalizationdeffileencoding = null;  

## Transaction Reports
public static int transactionReportPageSize = 100;  


## Unknown

public static String defaultRegAffTypeUTC = null;  
  
public static int pushPlayerMessageLife = 10000;  
public static int msgAllChildAffiliates = 1;  
  
public static boolean autoActivateWebmasterRegistrations = true;  
  
public static String serverType = "game";  
public static long gdkEventTimeout = 30000;  
  
public static int numReservedGamePlayIdInBatch = 1000;  
public static int numReservedHandIdInBatch = 1000;  

## Game Profile Management System
  
// Properties for Game Profile Management System.  
public static boolean updateCache = false;  
public static int maxNumberGameProfiles = 2000;  
public static int maxSizeXmlContent = 100000;  
public static int maxNumberPJPlans = 500;  
public static String gigaSpaceMapURL = null;  
## Event Space GigaSpace 

// EventSpace/GigaSpace section  
public static String esGigaSpaceURL = null;  
public static String esDAOClassName = null;  
public static String esErrorHandlerClassName = null;  
public static String esLogEventsDestination = "NONE";  
public static int esMaxResetEvents = -1;  
public static int esMaxHandlers = -1;  
public static int esSpaceRetries = -1;  
public static long esSpaceOperationWaitTime = -1;  
public static long esSpaceTransactionLeaseTime = -1;  
public static long esReaperSleepTime = -1l;  
public static int esEventHandlerLeaseTime = -1;  
public static int esEventHandlerErrorLimit = -1;  
public static long esEventHandlerDownTime = -1l;  
public static long esEventHandlerSleepTime = -1l;  
public static int esErrorHandlerLeaseTime = -1;  
public static long esErrorHandlerSleepTime = -1l;  
public static int esServerPort = 80;  // (ys) change to 80 from 8080 for TT23238, as down the road, cgs will be more on standalone deployment  
  
public static long esEventEndTicketTTL = 60L * 24L * 60L * 60L * 1000L; //60 days  
public static long esEventStartTicketTTL = 10L * 24L * 60L * 60L * 1000L; //10 days  
  
public static int esFeederMaxHashGroups = -1;  
public static int esFeederMaxEventLoad = -1;  
public static long esFeederMaxAllowedEvents = -1l;  
public static long esFeederLeaseTime = -1l;  
public static long esFeederSleepTime = -1l;  
public static boolean esEventTimeHistory = false;  
  
  
public static String cwhGigaSpaceURL = null;  
public static int csMaxProcessingObserverTasks = 5;  
public static long csCacheStateMonitorSleepTime = 1000l;  
public static boolean playerExclusionPassword = false;  
public static boolean depositLimitPassword = true;  

## XML sanitization
  
public static boolean cleanupReqXmlEnabled = false;  

 * Controls sanity clean-up measures of incoming XML requests from legacy games (Casino 1.0). * Setting this value to TRUE causes CasinoDocument.createRequest to trim leading chars prior to * the XML declaration and trailing chars from the closing root tag.  Set this value using the * property name 'base.cleanupReqXml.enabled' in the CasinoProperties table. * * @author awilson TT15546  
 * @since 2008-09-17  

public static final String CLEANUP_REQ_XML_ENABLED = "base.cleanupReqXml.enabled";  

 * Property name for cleanupReqXmlEnabled, 'base.cleanupReqXml.enabled'. * * @author awilson TT15546  
 * @since 2008-09-17  
  
## Messaging 

public static int messageMaxHashGroups = -1;  
public static long messageFeederSleepTime = 100l;  
public static int messageFeederSleepTimeMultiplier = 10;  
public static int messageFeederMaxReads = -1;  
public static long messageMonitorLowWaterMark = -1l;  
public static int messageMaxSeq = -1;  
public static long messageMonitorSleepTime = -1l;  
public static long messageWaitingTimeout = 30000l;  
public static boolean messageKeepAlive = true;  
public static long lastMessageValidationInterval = 60000L;  
  
## Xmpp (Chat)
public static String xmppserveraddress = null; // IP or Domain  
public static String xmppserveradmin = "admin";  
public static String xmppserverpassword = "chatpassword";  
public static Boolean xmppserverenabled = false;  
public static String xmppConsoleURI = null;  
public static int xmppConnectionEstablishTimeout = 5000;  
public static int xmppConnectionActiveTimeout = 20 * 1000;  
public static int xmppConnectionWaitTimeout = 5000;  
public static int xmppConnectionIdleTimeout = 5 * 60 * 1000;  
public static int xmppMaxQueueSize = 300;  
public static int xmppMaxConnection = 5;  



  
## Stateless Games  
public static boolean game_session_stateless = false;      
public static String data_repository_factory;  
public static int num_expired_sessions_retrieved = 100;  
  
public static int game_session_cleanup_numRowPerBatch = 100;  
public static int game_session_cleanup_numOfBatch = 200;  
public static int game_session_cleanup_sleep_ms = 15000;      
public static boolean game_session_single_game = false;          
  
public static boolean game_event_messaging = false;  
public static boolean game_event_messaging_bet = false;  
public static boolean game_event_messaging_win = false;  
  
public static boolean game_event_messaging_new = false;  
public static boolean game_event_messaging_bet_new = false;  
public static boolean game_event_messaging_win_new = false;  
  
public static boolean game_event_messaging_pff = false;  
  
//We will cache the game profile contents in memory but will perform refresh check periodically. //Default value is 5 minutes.  
public static long game_profile_cache_refresh_interval = 5 * 60 * 1000;  
  
public static int remote_game_connection_timeout_ms = 30000;  
  
public static String geoIPUrl = "";  
  
public static boolean rngLog = true;
## Misc
- `siteParent`
- `gameSite`
- `casinoEntry`
- `supportRecipient`
- `casinotimeout`
- `inactivetimeout`
- `icdtimeout`
- `siteName`
- `appletPath` - #why ? Is it still in use?
- `gameWidth`
- `gameHeight`
- `licenseeLSDID` #field/lsdId 
- `deployIp`
- `casinoDownloadProductId`
- `casinoDownloadInstallerName`
- `gameSessionProcessingTimeout`
	- this is the expiration time of a game session. 
	- If a game request is stuck for this time, the game session will be considered expired and will be cleaned up.
- 
