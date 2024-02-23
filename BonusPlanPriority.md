---
class: BonusPlanPriority
package: com.ttg.platform.core.domain.BonusPlanPriorityy
module: cgs
submodule: cip
---

Fields
- id
- #field/bonusCode  but #why here AND in [[BonusPlan]]?
- #field/bonusCode 
- name
- priority
In `PlayerFreeGamesBonusPlanCommand` a `com.ttg.platform.core.domain.BonusPlan` object is returned with a priority set to 1, but there is no `BonusPlanPriority` object in that object. The priority is represented as a simple int, although the 