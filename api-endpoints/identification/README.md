# Identification

Idfy lets you identify your users using our REST API or the OpenID Connect standard. See the comparision below to find out which of these options best suit your needs.

## [OpenID Connect](openid-connect.md)

**Pros**

* Industry standard
* Supported by many libraries and framework
* Great for JavaScript clients where API keys cannot be protect from end-users

**Cons**

* Currently no iframe support
* Higher entrace level, the developer has to read up on the spec and various flows

## [REST API](rest-api-flow/)

**Pros**

* Easy to get started, requires only a few API calls
* SDK available for many langauges
* Supports iframe

**Cons**

* Propraitary protocol, you have to implement your own flow

