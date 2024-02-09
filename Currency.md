Class that handles currencies in app. It is not just a simple label holder. It also holds a `curRate` because it is used in [[CurrencyRate]] .  CurrencyRate only has siteCurrency and a List(Currency), so I am assuming that `curRate` is there to hold the current Currency's rate relative to the site's currency. 
Fields
- id
- #field/curName
- curDescription
- #field/curCode
- defCur
- modifiedByGid
- defaultAccId
	- This is the id for the default [[Account]] for this currency
- #field/curRate
- lastModified
- baseCurCode #what
- active: Boolean
- curCountry (String)
	- #why String and not Country?