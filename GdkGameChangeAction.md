`com.cwh.gdk.common.pojo.GdkGameChangeAction`

See [[GameProfile]] for an explanation of the functionality.
Fields:
- autocomplete: boolean
	- Should the system should perform autocomplete when a game profile is de-activated or not?
- autoCompleteRequest
	- which request defines the end of a gameRound?
- changeUpdator: Class(? extends [[GdkGameChangeHistoricalDataUpdater]])
	- this class is reponsible for updating [[Historical Data]] after [[Game processing| default game processing]] is completed