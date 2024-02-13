This is an interface in `com.cwh.gdk.common.pojo`. 
From what I can see, there is a single implementation, LottoGameChangeHistoricalDataUpdater.
# Methods
## suspendUpdate
Takes as parameter [[GdkHistoricalDataInterface]], [[GdkRegister]] and a set of refundGameKeys (Long). 

This is the method called after default [[Suspend action|suspend actions]] have been performed

## resumeUpdate
Takes as parameter [[GdkHistoricalDataInterface]], [[GdkRegister]]. It is not called anywhere that I can see.