---
tags:
  - business/identity
---


How is a [[Player]]'s identity determined? Throughout the #legacy application, it is usually done using playerId, presumably the same value from the database. But the goal is to determine the player's business identity throughout the application. While #field/playerId is useful to establish some business concepts, there may be other contexts in which different techniques of identifying the user might be used.