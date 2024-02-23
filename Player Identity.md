---
tags:
  - business/identity
---


How is a [[Player]]'s identity determined? Throughout the #legacy application, it is usually done using playerId, presumably the same value from the database. But the goal is to determine the player's business identity throughout the application. While #field/playerId is useful to establish some business concepts, there may be other contexts in which different techniques of identifying the user might be used.

In `com.ttg.platform.core.dao.mapper.PlayerMapper` there are several select clauses for the #field/playerId . 
```sql
SELECT playerId FROM Player WITH (NOLOCK) WHERE clientAccount = cast(#{clientAcct} as varchar(512)) AND siteID=#{siteId}

SELECT playerId FROM Player WITH (NOLOCK) WHERE nickname=#{nickname} AND siteId=#{siteId}

SELECT playerId FROM Player WITH (NOLOCK) WHERE username=#{username} AND siteId=#{siteId}
```

So a player's uniqueness is determined by username, nickname and #field/clientAccount, together with the siteId. But why not use the player's username from the start, or some UUID used throughout to identify the player? 

#dbproc/proc_createCasinoPlayer creates a Player, but maps the table columns in a weird way. 
- It inserts in #table/UserPreferences (userId) the playerId passed as parameter (it is previously generated in java code by calling a sequence)
- then inserts the rest of the user details in #table/Player
- but then it also inserts values in #table/PlayerStatus with `statusId=1`
- inserts in #table/RealityCheckState (playerId,rcFlag) the player's id, and 0 (so reality check is not used or the user can's set it when he creates an account?)
- inserts into #table/VCtoCC (vcaccid,ccuserid,siteId) (player's client account, the player's Id/also userId, and the siteId )
- inserts into #table/Password (passwordId, encryptedPwd) (user id, also user Id) #fml #what 
- inserts into #table/PlayerInfo (playerId, countryId,modifiedByGid) values (userId, "XX", modifiedByGid), the latter also a parameter. But why XX instead of country?
- Then handles player confirmation #table/PlayerConfirmation
