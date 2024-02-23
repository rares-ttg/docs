This is the business identity of an [[Affiliate]]. While most often an affiliate is referenced by #field/affId , there are references to #field/loginAffId #field/regAffId #field/calcAffId 

In [[CIP]] `FreeGameEligibilityService` there is a method called `constructFreeGameEligibilityRequest` which gets an #field/affId  from #field/lsdId and #field/siteId . The method called is `com.ttg.affiliate.dao.AffiliateDAO.getAffiliateId` which uses a MyBatis mapper to run the following select on #table/Affiliate :
```sql
SELECT affId FROM AFFILIATE WITH (NOLOCK) WHERE lsdId = #{lsdId} AND siteId=#{siteId}
```

So it is safe to assume that an Affiliate's identity is given by `lsdId`, which is assigned manually and a `siteId`.

SiteId is a system identifier in case you have multiple systems so you know which system the accounting data comes from. This is the regulated mode, in which siteId is an identifier for different licensing terms and requirements. In unregulated mode, such details are ignored. It is more of a reference to an environment, rather than an actual site. An affiliate can function under several siteId's, hence why you need to select for both `lsdId` and `siteId`


## Registration Affiliate Id

This is what is meant by #field/regAffId 
## Calculated Affiliate Id

This is #field/calcAffId , and is used in [[Rule of Affiliate Transaction Tagging|RATT]]. 

## Login Affiliate Id

Also used in [[RATT]] 