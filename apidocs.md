# Introduction
The Idfy API is a RESTful API that use the OAuth 2.0 protocol for authorization. All request and response bodies are formatted in JSON.

# Getting started

## Get an account
To use the API you need an account at Idfy. You can get a free test account by signing up through our [onboarding site](https://onboard.idfy.io).

## Support
We’re here to help! Get in touch with support at support@idfy.io and we’ll get back to you as soon as we can.

# Authentication
This API uses OAuth2 for authentication. OAuth2 - an open protocol to allow secure authorization in a simple and standard method from web, mobile and desktop applications. Be sure to use `client_credentials` as grant type when connecting to this API. 

## Obtaining an access token

An access token can be obtained by making a request to the OAuth2 token endpoint.

The request must include the following parameters:

| Parameter | Value |
|----------|----------|
| `grant_type` | The type of grant used to authenticate the request. In this case: `client_credentials`. |
| `scope` | Space-delimited list of requested scope permissions. |

Example:

```
POST https://api.idfy.io/oauth/connect/token
Content-Type: application/x-www-form-urlencoded
Authorization: Basic Y2xpZW50SWQ6Y2xpZW50U2VjcmV0
 
grant_type=client_credentials
scope=document_read
```

**Note**: This request must authenticate using HTTP basic authentication with your *Client Id* as the username and *Client Secret* as the password. The format is the base-64 encoded string `client_id:client_secret`.  

If your credentials are valid, the server will respond with a JSON body containing the access token and its expiration time:
```
{
    "access_token": "xxxxx.yyyyy.zzzzz",
    "expires_in": 3600,
    "token_type": "Bearer"
}
```

You can now store and use the access token to make authenticated request by passing it as an authentication header:

`Authorization: Bearer xxxxx.yyyyy.zzzzz`

You can read more about OAuth2 [here](https://www.digitalocean.com/community/tutorials/an-introduction-to-oauth-2).

# REST API

## HTTP status codes
* `200 OK`: The request was successful.
* `201 Created`: A new resource was successfully created.
* `204 No content`: The request was successful but returns no body.
* `400 Bad request`: The request was invalid, often due to missing a required parameter.
* `401 Unauthorized`: Authentication failed due to invalid credentials.
* `402 Payment Required`: The endpoint is not accessible in your current subscription. Contact sales@idfy.io.
* `403 Forbidden`: Authorization failed due to insufficient scope/access.
* `404 Not found`: The specified resource does not exist.
* `422 Unprocessable Entity`: The server understood the request, but was unable to process it due to a business or logical error (For example creating an XML signature with Swedish BankID which is not supported).
* `429 Too Many Requests`: The request was blocked due to rate limiting.
* `500 Internal Server Error`: An internal server error occured.
* `503 Service Unavailable`: A third party service that this endpoint depends on caused an error or is unavailable.

## HTTP verbs
* `GET`: Retrieves a resource or lists resources.
* `POST`: Creates or exceutes a commandand on a resource.
* `PUT`: Replaces a resource.
* `PATCH`: Partially updates a resoruce.
* `DELETE`: Deletes a resoure.

## Formats
The Idfy API only supports JSON format. All request must use the `Content-type` header set to `application/json`. The JSON will use camelCasing. All request must use the UTF-8 encoding, and all responsens will be in UTF-8.
All file download wills be a standard HTTP download result.

## Idempotent Requests
The APIs supports idempotency for safely retrying requests without accidentally performing the same operation twice. For example, if a request to create a new document fails due to a network connection error, you can retry the request with the same ExternalId  to guarantee that only a single document/identification is created.

## Compatibility
The Idfy API do change from time to time, but all changes will follow strict rules in order to keep the API's backward compatible. All new fields will be optional, and if large changes are required a new endpoint will be created. If an endpoint is being deprecated, all customers will be given notice well in advance.

## Pagination (linked lists)
When using paging the list will be wrapped in a linked list object. The data contains the list-data in the result. There will also be navigation links for next, first, last and previous page. The total amount of results (size) will also be inlcuded.
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
      {
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

## HTTP response headers
All API request have some standard HTTP headers:
* `X-Idfy-Environment`: (test or prod) this header tells you if you are talking to the test or the production environment.
* `X-Idfy-AccountId`: The Idfy accountID for the request.
* `RequestId`: Each API request has an associated request identifier. You will also be able to use this to search in the logs in the Idfy dashboard. If you need to contact us about a specific request, providing the request identifier will ensure the fastest possible resolution.

# Status page
Visit our [status page](https://developer.idfy.io/status) if you want to know the status of our services or subscribe to notifications.

<!-- ReDoc-Inject: <security-definitions> -->
