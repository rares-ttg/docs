---
tags:
  - legacy
  - "#table/Game_Group"
  - "#code"
---
A game group seems to be a way to group [[Game|games]] for some technical purposes, as there is no `GameGroup` class declared. In `com.cwh.xboss.tasks.clientWeb.PlayerProfileSummaryTask` there's a `SELECT` with a `WHERE` clause in which #table/Game_Group groupName is restricted to Poker and [[Tournament]].  

Game groups are the kinds of games that you can play in the casino. The main groups
- [[Slots]]
- [[Video Poker]]
- Table
- [[Bingo]]
In `GameConnector`, there is a select which selects only games where #field/groupName is `SLOTS, VIDEOPOKER,TABLE OR BINGO`