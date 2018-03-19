# Authentication

We support two different authentication flows. You could choose between using our REST API or the OpenID Connect standard.

See the comparision below to find out whats best suits your need.

## OpenID Connect
### Pros
* Industry standard
* Supported in many libraries and framework
* Can be used in javascript client where API keys are not possible to protect.

### Cons
* Do not support iframes (There may be support for this in the future)
* Higher entrace level, the developer have to read up on the spec and the flow of the standard.

## Idfy REST API
### Pros
* Simpler just download the client library and make the call. (See further down for the flow)
* Supports iFrame

### Cons
* Propraitary protocol have to write your own flow.

## Using the Idfy REST API
To use the Idfy api apply the following steps:

1. Create this returns a url and a sessionId. Store the sessionid on the server and redirect to the url or embed the url in a iFrame tag. In the request you supply successurl, errorurl, aborturl, and the identityprovider to use (NoBankID, SweBankID among others)
2. The user authenticates using the choosen identityprovider and is redirected back to your site.
3. Call our api using the SessionID from step 1, get information aboute the user, identityprovider id, socicalsecuritynumber (if your allowed to), name etc.
4. (Optional) Call our api and invalidate the session this is a protection against replay attacks.

## Using OpenID Connect
Log on to our dashboard and create an OpenID Connect client, choose the OpenID connect flow that suits you usecase. If you are not sure what flow to use read this guide by one of the experts in the field: <a href="https://leastprivilege.com/2016/01/17/which-openid-connectoauth-2-o-flow-is-the-right-one/" target="_blank">https://leastprivilege.com/2016/01/17/which-openid-connectoauth-2-o-flow-is-the-right-one/</a>. The use the following OpenID endpoints:
 * Test: https://oauth2test.signere.com
 * Production https://oauth.signere.no
