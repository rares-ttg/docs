---
module: games
submodule: casino
package: com.cwh.gdk.servlet
class: GdkCasinoServlet
tags:
  - "#code"
---
Only handles Post 

The overall architecture is as follows:

> `doPost`->`GdkCasinoServletSupport.processGdkRequest(GdkRequest)`->`GdkCasinoServletSupport.callCmd(GdkRequest,Connection, GdkGameSessionDataRepositoryProcessor, GdkSystemCmdProcessor)`-> `GdkCmdFactory->getCdkCmd(GdkRequest)`->`GdkGameCmd.execute(Connection,GdkRequest)` OR `GdkSystemCmd.execute(Connection,GdkRequest)`-> `cmd=GdkRequest.getGameSettings().getRuleClass()`->`gcmd=Class.forName(cmd).newInstance()`->`rule=gcmd.getGameRule(userId,GdkRequest.getReqData())`-> `GdkGameRuleInterface.processRequest(int userId,jdom.Element request, jdom.Element profile, HashMap states, HashMap singleStates, GdkHistoricalDataInterface,GdkRandomGenerator)`