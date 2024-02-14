# CGSLib

The following are from cgs lib, the `com.cwh` packages. I assume they have to do with the common wallet. 
## Create Banner

see `com.cwh.xboss.tasks.affcomp.AddBannerTask`. It creates the banner, it does not assign it.
## [[Compensation Package]]
### Add [[Compensation Package]] to an Affiliate

`com.cwh.xboss.tasks.affcomp.AddRemoveCompPkgTask`

### Remove [[Compensation Package]]

`com.cwh.xboss.tasks.affcomp.AddRemoveCompPkgTask`

### Create [[Compensation Package]]

`com.cwh.xboss.tasks.affcomp.CreateCompPkgTask`

### Assign [[Compensation Package]] to an [[Affiliate]]

### Retrieve [[Compensation Package]] usage

## Search Affiliates

`com.cwh.xboss.tasks.affcomp.AffListSearchTask`

Search for all affiliate information for a hierarchy of affiliates that the user has #permission to view. It has a flag to determine whether to include inactive affiliates 

## Get Earnings by Day Report

## Pay [[Affiliate]] 

Decreases the amount earned balance and increases the amount paid balance of an account type belonging to an Affiliate. The amount of the payment must be zero or greater. #why couldn't it be both pay and get paid? is it because affiliates do not make payments towards ttgs?

## View [[Affiliate Account]]

