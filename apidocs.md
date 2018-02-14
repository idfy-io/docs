# Introduction
[intro]

# Getting started
## Get an account
To use the API, you need an API account at Idfy You can get a free test account by going to our onboarding site and filling out the form there: [https://onboard.idfy.io](https://onboard.idfy.io) 
## Support
We’re here to help. Get in touch and we’ll get back to you as soon as we can. [Contact us](support@idfy.io).


[sitecontent]

# Statuspage
If you want to know the status of our services or subscribe to notifications go to our Statuspage: [http://signere.statuspage.io/](http://signere.statuspage.io/)

# REST API

## Statuscodes
* 200 OK: Everything worked as expected.
* 201 Created: New resource is created for example a new document for signing.
* 204 No content: The response code when a resource is deleted.
* 400 Bad request: The request was unacceptable, often due to missing a required parameter, or parameter not following given restrictions.
* 401 Unauthorized: Not authorized for this API
* 402 Payment Required: When trying to access an endpoint that are not in your current subscription. Contact sales@idfy.io.
* 403 Forbidden: Not correct scope/access to this resource
* 422 Unprocessable Entity: The request syntax is correct, but there is a business or logical error. For example sign xml signature with Swedish BankID that is not supported.
* 404 Not found: The route is not found or the entity is not found. Look at the reason phrase in the response to find detailed error.
* 429 Too Many Requests: The API have built in throttling to prevent any singel customer taking the API down.
* 503 Service Unavailable: A 3rd party services that this endpoint uses had an error or is unavailable.
* 50x Server errors: Something is wrong on the Idfy servers or the hosting environment.

## Http verbs
* Get: Get a resource
* Post: Create a new resource or exceute a command on the resource that is only can be exceuted once.
* Put: Replace a resource or exceute a command on the resource that is only can be exceuted mulitple times.
* Patch: Partially update a resoruce.
* Delete: Delete a resoure.

## Formats
The Idfy API only support json format at the time beeing. All request must use the Content-type header set top application/json. The json will use camelCasing. All request must use the UTF-8 encoding. All responsens will be in UTF-8.
All file download will be a standard http download result.

## Idempotent Requests
The APIs supports idempotency for safely retrying requests without accidentally performing the same operation twice. For example, if a request to create a new document fails due to a network connection error, you can retry the request with the same ExternalId  to guarantee that only a single document/identification is created.

## Compatibility
The Idfy API do change from time to time, but all changes will follow strict rules in order to keep the API's backward compatible. All new fields will be optional never required and if large changes are required a new endpoint will be created or a new API.
If an API are to be deprecated all customers will be given notice well in advance and not shutdown until all customers have converted to the new API's.

## Pagination (linked lists)
When using paging the list will be wrapped in a linked list object. The data contains the list-data in the result. There will also be navigation links for next, first, last and previous. The total amount of results (size) will also be inlcuded.
Example:
```json
{
   "offset": 0,
   "limit": 2,
   "size": 45,
   "links": {
     "next": "https://api.idfy.io/signature/documents/summary?limit=2&offset=2",
     "first": "https://api.idfy.io/signature/documents/summary?limit=2",
     "last": "",
     "previous": ""
   },
   "data": [
      "id": "2519011552909132317BrJ6VqOrcBYfwmgQ2eypM5XP7DEbCm8",
      "name": "Bruce Wayne",
      "status": "SUCCESS",
      "clientIp": "192.168.1.1",
      "userAgent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.36",
      "identityProviderType": "NO_BANKID_WEB",
      "language": "NO",
      "externalid": "gtWEH8euBHeSWPTcjwB0Bg5o1mjsH106wmjTDMxoFnadzvNSsnSSY0zbJTpy",
      "timestamp": "2017-07-19T18:29:53.7550972Z",
      "iframe": false,
      "socialSecurityNumber": false
    },
    {
      "id": "2519011552909132317BrJ6VqOrcBYfwmgQ2eypM5XP7DEbCm8",
      "name": "Joker",
      "status": "ERROR",
      "clientIp": "192.168.1.1",
      "userAgent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.36",
      "identityProviderType": "FI_TUPAS",
      "language": "NO",
      "externalid": "gtWEH8euBHeSWPTcjwB0Bg5o1mjsH106wmjTDMxoFnadzvNSsnSSY0zbJTpy",
      "errorcode": "TIMEOUT",
      "timestamp": "2017-07-19T18:29:53.7550972Z",
      "iframe": false,
      "socialSecurityNumber": false
    }
  ]
}
```

## Http Response headers
All API request have some standard http headers theese are:
* X-Idfy-Environment: (test or prod) this header tells you if you are talking to the test or the production environment.
* X-Idfy-AccountId: The Idfy accountID for the request.
* RequestId: Each API request has an associated request identifier. You can find this value in the response headers, under Request-Id. You will also be able to use this to search in the logs in the Idfy dashboard. If you need to contact us about a specific request, providing the request identifier will ensure the fastest possible resolution.

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

