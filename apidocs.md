# Introduction
[intro]

# Getting started
## Get an account
To use the API, you need an API account at Idfy You can get a free test account by going to our onboarding site and filling out the form there: [https://onboard.signere.no](https://onboard.signere.no) 

[sitecontent]

# Statuspage
If you want to know the status of our services or subscribe to notifications go to our Statuspage: [http://signere.statuspage.io/](http://signere.statuspage.io/)
# API Authentication
This API uses OAuth2 for authentication the requests. OAuth2 - an open protocol to allow secure authorization in a simple and standard method from web, mobile and desktop applications. Be sure to use client_credentials as grant type when connecting to this API. 

<b>Simple step by step guide to receive required access token </b><br/><br/>
1) Get access token <br/><br/>
http POST to https://oauth2test.signere.com/connect/token for test or https://oauth.signere.no/connect/token for prod <br/><br/>
&bull; Request Headers: <br/>
&nbsp;&nbsp;Content-Type: application/x-www-form-urlencoded <br/>
&nbsp;&nbsp;Authorization: Basic auth with ClientId as username, and ClientSecret as password<br/>
&nbsp;&nbsp;<i>Pseudo code: Authorization: "[ClientId]:[Secret]".ToBase64String() (utf-8) </i> <br/>
<br>
&bull; Request Body:<br/>
&nbsp;&nbsp;grant_type: client_credentials<br/>
&nbsp;&nbsp;scope: [insert scope(s) here] (Contact us if you dont have access to this scope) <br/>
<br>
2) Use access token to access our API<br/><br/>
In the response you will receive an item containing the id token you should use to connect to our API's named access_token.<br/>
&bull; This token can then be added to the header in the requests to this API:<br/> 
&nbsp;&nbsp; Authorization: Bearer [access_token]
<br><br>
We have created a guide to create Oauth2 tokens for different languages here: [https://sdk.signere.com/oauthtoken.html](https://sdk.signere.com/oauthtoken.html)
<br><br><i>Hint: The access token has a limited lifetime, check how long it will live in the response. Then you can save it to cache and reuse it (our .NET nuget client does this for you)</i><br><br>
Read more aboute OAuth2 here: 
[https://www.digitalocean.com/community/tutorials/an-introduction-to-oauth-2](https://www.digitalocean.com/community/tutorials/an-introduction-to-oauth-2)
<!-- ReDoc-Inject: <security-definitions> -->

