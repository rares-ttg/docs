---
aliases:
  - CBUser
---


This seems to stand for a many-to-many table between #field/siteId and #field/affId  (both integers). Can an [[Affiliate]] have more than one site, and can a site belong to more than one Affiliate?  
- [ ] What is the relation between Casino operator and CBUser? The latter is presented as a casino user
- [ ] do casino users have access only to specific affiliates, or can they see all of them? for this, see `PlayerFreeGamesBonusPlanCommand.getBonusAwardFromBonusPlan`