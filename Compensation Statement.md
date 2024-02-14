---
class: CompStmt
package: com.cwh.xboss.tasks.affcomp
module: cgs
submodule: cgslib
tags:
  - legacy
  - "#code"
---
It is part of a [[Compensation Package]]. It has a min and max value and an amount that is applied iff the amount of(?) hold is between those values

## Fields

- `int compStmtId`
- [[Money]] `amt` - the amount
- `int minVal`
- `int maxVal`
## Construction

It can be constructed from a compStmtId if one already exist, or from an amount, minVal and maxVal

