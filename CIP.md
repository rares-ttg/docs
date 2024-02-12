---
tags:
  - module
---
# Overview
Location relative to root `cgs` project folder: `webapps/cip`.
It is a jersey REST service. The endpoints are in package `com.ttg.cip.rest.service`. They all inherit from `BaseService` which is in the same package, which also inherits `com.ttg.rest.service.CoreService` (outside `cip` package). `CoreService` has a reference to an ibatis SqlSessionManager which it gets from a guice `Injector` used in a totally absurd way. 

# Paths

## /login

This is handled in `AffiliateLoginService`

### Request

A request can be a regular request, or a `T24` request, whatever that is 

#### Headers
The headers must contain the [[Affiliate|affiliate's]] username (`Affiliate-Id`) and the affiliate's password (`Affiliate-Login`).  If it is a `T24` request, then the headers have a `T24-` prefix.

### Process

The credentials, as they should've been called, are then sent to an `AffiliateAuthenticationCommand`, which is in [[ttglib]] and checks the credentials, somehow. Returns a token if it exists, or a new token otherwise.
- [ ] [CIP]Really look into how the credentials are checked.
### Response

There are regular responses, and `T24` responses, corresponding to the same kind of requests. The response headers contain the token, the expiration date, and whether it is a new token or not. So, the headers are
- `Affiliate-Granted-Token`
- `Affiliate-Granted-Token-Expiry`
- `Affiliate-New-Token-Granted`, values yes/no.
with `T24-` prefix for `T24` requests
### Dependencies

Depends on [[com.ttg.security.command]] in [[ttglib]]

## /freegame/eligibility

Handled by `FreeGameEligibilityService`. 

Checks whether the affiliate is eligible for a free game, using the affiliate's authentication details. 

### Dependencies

Also on [[ttglib]] via [[com.ttg.security.command]].

## /freeSpins

Handled by `FreeSpinsService`.
### /freeSpins/get

Contrary to its name, this is a `POST` request, because reasons. 
Input, this is in `FreeSpinGetRequest`: 
- clientAccount
- siteId
- lsdId

### /freeSpins/add


