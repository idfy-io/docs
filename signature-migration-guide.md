# Signature migration guide

## Migration guide

New API docs: [https://docs.idfy.io/api-endpoints/sign](https://docs.idfy.io/api-endpoints/sign) Api reference: [https://developer.idfy.io/api\#tag/Signature-Endpoint](https://developer.idfy.io/api#tag/Signature-Endpoint)

Our legacy sign API will be shut down in the end of the year \(2018\), please migrate to our new API as soon as possible.

#### Important note

This guide is under development and is lacking information, please contact support if you need assistance.

**Why upgrade?**

If you want to continue using our signature services you should start using our newest API as soon as possible for the following reasons:

* It's a more modern Rest API
* A lot of new features you can read more about below
* Once you start using it, it is much easier to understand than our legacy API

**New features in our new API**

* Multiple eid providers
* Customizable GUI
* Oauth 2 authentication
* Test/Prod environment uses the same API endpoint \(just change the oauth client\)
* Required number of signatures, sign orders, mark one or more signers as required \(prokura\)
* Attachments \(both signable and to be viewed/accepted\)
* All signers can sign simultaneously
* Mobile sign for norwegian bankid
* And more

**Features in development**

* Multidocument signing
* "Eaccept" - Sign the document with a eid login / sms otp / passport + a handwritten signature
* And more

**Breaking changes**

* New API Authentication \(Oauth 2.0\)
* Document lifetime \(the documents will be deleted on our side max 7 days after the document is signed or is expired\)
* New API endpoints
* New API models \(Shares many of the legacy features\)

#### 

#### First step: Add oauth authentication

Read how to implement this here:

[API Authentication](/api-authentication.md)

If you dont have access to your oauth credentials please retrieve them from the Idfy dashboard or contact support@idfy.io.

#### What happened to all the different endpoints to create a document?

We decided to have the same endpoint regardless if you are using an iframe, link and/or email/sms. You just have to specify how you want it to be handled: [https://docs.idfy.io/api-endpoints/sign/events-redirect-settings-and-files/redirect-settings-and-webmessages](https://docs.idfy.io/api-endpoints/sign/events-redirect-settings-and-files/redirect-settings-and-webmessages)

#### Webhooks / Event client

If you are using / want to implement webhooks or our .net event client, this is also in a new improved form. Read more about it here: [https://docs.idfy.io/api-endpoints/notification](https://docs.idfy.io/api-endpoints/notification)

