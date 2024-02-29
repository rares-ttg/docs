---
tags:
  - "#legacy"
  - "#game-collection"
aliases:
  - CGS casino
module: games
---

It is part of [[CGS]]. 
For each game there is an implementation of the `casino.server.ServerGame` class.
There are 33 games:
1. Slots
	1. [[Arthur's Quest]]
	2. [[Five Reel Slots]]
	3. [[Fast Track]]
	4. [[Fruit Party]]
	5. [[Bulls Eye Bucks]]
	6. [[Generic Slots]]
	7. [[Hollywood Reels]]
	8. [[Hole in One]]
	9. [[Oktoberfest]]
	10. [[Slots]]
2. Cards
	1. Black Jack
		1. [[BlackJack]]
		2. [[BlackJack No Commission]]
		3. [[Euro Black Jack]]
		4. [[Lucky7 BlackJack]]
		5. [[Euro Black Jack]]
		6. [[Pickem BlackJack]]
		7. [[SD BlackJack]]
		8. [[BlackJack No Commission]]
	2. Poker
		1. [[Casino Stud Poker]]
		2. [[Pai Gow Poker]]
		3. [[Trey Poker]]
		4. [[Three Cards Poker]]
		5. [[Video Poker]]
			1. [[Jacks or Better No Comission]]
		6. 
	3. [[Baccarat]]
		1. [[Baccarat Zero Commision]]
	4. [[Battle Cards]]
	5. [[Red Dog]]
	6. [[Casino War]]
3. Dice Games
	1. [[Craps]]
	2. [[Sic Bo]]
4. Roulette
	1. [[Euro Roulette]]
	2. [[Roulette]]
	3. [[Roulette No Comission]]
5. Lotto
	1. [[Pulltab]]

## Main structure
### Game Servlets

There are 5 servlets associated:
- CasinoFlashServlet - #deprecated 
- [[GdkCasinoServlet]]
- `com.chartwelltechnology.servlet.game.CasinoServlet`
- `com.cwh.gdk.GamingServlet`


The order of instantiation, as described in `web.xml` is 
1. CasinoServlet
2. CasinoFlashServlet
3. GdkCasinoServlet
4. GamingServlet

## Servlet list

| Servlet Name                 | URL mapping                                                                  | Init order |
| ---------------------------- | ---------------------------------------------------------------------------- | ---------- |
| jersey-servlet               | /rest/*                                                                      | 1          |
| CasinoServlet                | /servlet/CasinoServlet                                                       | 1          |
| CasinoFlashServlet           | /servlet/CasinoFlashServlet                                                  | 2          |
| GdkCasinoServlet             | /servlet/GdkCasinoServlet                                                    | 3          |
| RemoteInitializeServlet      | /servlet/RemoteInitializeServlet                                             | 10         |
| ResourceServlet              | /servlet/ResourceServlet                                                     | 11         |
| MonitoringServlet            | /servlet/MonitoringServlet                                                   | 20         |
| GamingServlet                | /servlet/GamingServlet                                                       | 22         |
| GameEndServlet               | /servlet/GameEndServlet                                                      |            |
| AboutServlet                 | /servlet/AboutServlet                                                        |            |
| DownloadInstallerServlet     | /servlet/DownloadInstallerServlet                                            |            |
| gw                           | /servlet/gw                                                                  | 23         |
| PublicKeyServlet             | /servlet/PublicKeyServlet                                                    |            |
| MessaginServerStartupServlet | /servlet/MessaginServerStartupServlet                                        |            |
| ParticipantGetEventServlet   | /servlet/ParticipantGetEventServlet                                          |            |
| ActivateCodedBonusServlet    | /servlet/ActivateCodedBonusServlet                                           |            |
| BestRunServlet               | /servlet/BestRunServlet                                                      |            |
| DictionaryServlet            | /servlet/DictionaryServlet                                                   |            |
| DownloadLoginServlet         | /servlet/DownloadLoginServlet                                                |            |
| DownloadModuleServlet        | /servlet/DownloadModuleServlet                                               |            |
| DownloadTrackingServlet      | /servlet/com.chartwelltechnology.servlet.download.DownloadTrackingServlet    |            |
| FlashDebugServlet            | /servlet/com.chartwelltechnology.servlet.game.FlashDebugServlet              |            |
| GameProfileListServlet       | /servlet/com.chartwelltechnology.icd.GameProfileListServlet                  |            |
| GameResumeServlet            |  /servlet/com.chartwelltechnology.icd.GameResumeServlet                      |            |
| EnvironmentSettingsServlet   |  /servlet/com.chartwelltechnology.icd.EnvironmentSettingsServlet             |            |
| GdkBlockReportServlet        | /servlet/com.cwh.gdk.servlet.GdkBlockReportServlet                           |            |
| LocalizationSupportServlet   | /servlet/com.chartwelltechnology.icd.LocalizationSupportServlet              |            |
| LoginServlet                 | /servlet/com.cwh.servlet.game.LoginServlet                                   |            |
| LogoutServlet                | /servlet/com.cwh.servlet.game.LogoutServlet                                  |            |
| MyAccountSupportServlet      | /servlet/com.chartwelltechnology.servlet.myaccount.MyAccountSupportServlet   |            |
| OperatorServlet              | /servlet/com.cwh.server.operator.OperatorServlet                             |            |
| PlayerInfoServlet            | /servlet/com.cwh.integration.type3.servlet.PlayerInfoServlet                 |            |
| ParticipantGetEventServlet   | /servlet/com.cwh.eventSpace.community.participant.ParticipantGetEventServlet |            |
| ProcessLoginServlet          | /servlet/com.chartwelltechnology.icd.ProcessLoginServlet                     |            |
| PublicKeyServlet             | /servlet/com.cwh.messaging.server.PublicKeyServlet                           |            |
| RegistrationFormServlet      | /servlet/com.cwh.servlet.common.utc.RegistrationFormServlet                  |            |
| RegistrationFormServlet      | /servlet/com.cwh.servlet.common.utc.RegistrationFormServlet                  |            |
| PromotionServlet             | /servlet/com.chartwelltechnology.servlet.progressivejackpot.PromotionServlet |            |
| XRegistrationServlet         | /servlet/com.cwh.servlet.common.utc.XRegistrationServlet                     |            |
| DynamicFileServlet           | /servlet/DynamicFileServlet                                                  |            |
## Filter list

| Filter name                 | Filter class                                                   | Mapping |
| --------------------------- | -------------------------------------------------------------- | ------- |
| ConfigValidationFilter      | com.cwh.util.filter.ConfigValidationFilter                     |         |
| NoCacheServletFilter        | com.cwh.servlet.common.filters.NoCacheServletFilter            |         |
| GameContainerProxyFilter    | com.cwh.gdk.loader.servlet.filters.GameContainerProxyFilter    |         |
| GameResourceProxyFilter     | com.cwh.gdk.loader.servlet.filters.GameResourceProxyFilter     |         |
| ExternalResourceProxyFilter | com.cwh.gdk.loader.servlet.filters.ExternalResourceProxyFilter |         |
| DynamicFileFilter           | com.cwh.util.dff.DynamicFileFilter                             |         |
| CORS                        | com.thetransactioncompany.cors.CORSFilter                      |         |
