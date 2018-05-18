# Identification

Idfy lets you identify your users using our REST API or the OpenID Connect standard. See the comparision below to find out which of these options best suit your needs.

## OpenID Connect

**Pros**

* Industry standard
* Supported by many libraries and framework
* Great for JavaScript clients where API keys cannot be protect from end-users

**Cons**

* Does not support iframes
* Higher entrace level, the developer has to read up on the spec and various flows

## Idfy REST API

**Pros**

* Easy to get started, requires only a few API calls
* SDK available for many langauges
* Supports iframe

**Cons**

* Propraitary protocol, you have to implement your own flow

## Using the Idfy REST API

To use the Idfy API apply the following steps:

1. Create this returns a url and a sessionId. Store the sessionid on the server and redirect to the url or embed the url in a iFrame tag. In the request you supply successurl, errorurl, aborturl, and the identityprovider to use \(NoBankID, SweBankID among others\)
2. The user authenticates using the choosen identityprovider and is redirected back to your site.
3. Call our api using the SessionID from step 1, get information aboute the user, identityprovider id, socicalsecuritynumber \(if your allowed to\), name etc.
4. \(Optional\) Call our api and invalidate the session this is a protection against replay attacks.

## Using OpenID Connect

Log on to our dashboard and create an OpenID Connect client, choose the OpenID connect flow that suits you usecase. If you are not sure what flow to use read this guide by one of the experts in the field: [https://leastprivilege.com/2016/01/17/which-openid-connectoauth-2-o-flow-is-the-right-one/](https://leastprivilege.com/2016/01/17/which-openid-connectoauth-2-o-flow-is-the-right-one/). The use the following OpenID endpoints:

* Test: [https://oauth2test.signere.com](https://oauth2test.signere.com)
* Production [https://oauth.signere.no](https://oauth.signere.no)



