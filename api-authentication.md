# API Authentication

To access our API's you need to authenticate with the oauth 2.0 standard. OAuth2 - an open protocol to allow secure authorization in a simple and standard method from web, mobile and desktop applications. Be sure to use `client_credentials`as grant type when connecting.

## Endpoint

`https://api.idfy.io/oauth/connect/token`

Use this endpoint for both test and production environment.

## 1\) Obtaining an access token

An access token can be obtained by making a request to the OAuth2 token endpoint.

### Parameters

The request must include the following parameters:

| Parameter | Value |
| :--- | :--- |
| `grant_type` | The type of grant used to authenticate the request. In this case: `client_credentials`. |
| `scope` | Space-delimited list of requested scope permissions. |

Example

```text
POST https://api.idfy.io/oauth/connect/token
Content-Type: application/x-www-form-urlencoded
Authorization: Basic Y2xpZW50SWQ6Y2xpZW50U2VjcmV0

grant_type=client_credentials
scope=document_read
```

**Note**: This request must authenticate using HTTP basic authentication with your _Client Id_ as the username and _Client Secret_ as the password. The format is the base-64 encoded string `client_id:client_secret`

### Scopes

When you retrieve the access token you have to set which scopes you need, our API-enpoints requires different scopes.

A complete list can be found in our [API-reference](https://developer.idfy.io/api)

#### Our most used scopes:

| scope | Endpoint | Access level |
| :--- | :--- | :--- |
| document\_read | [signature](https://developer.idfy.io/api#tag/Signature-Endpoint) | Read access to documents |
| document\_write | [signature](https://developer.idfy.io/api#tag/Signature-Endpoint) | Write access to documents |
| document\_file | [signature](https://developer.idfy.io/api#tag/Signature-Endpoint) | Download files \(signed and unsigned\) |
| event | [notification](https://developer.idfy.io/api#tag/Notification-Endpoint) | Full access to [notification](https://developer.idfy.io/api#tag/Notification-Endpoint) endpint |
| identify | [identification ](https://developer.idfy.io/api#tag/Identification-Endpoint) | Read/Write access to [identification ](https://developer.idfy.io/api#tag/Identification-Endpoint)endpoint |

**Note:** The client you are using must be set up with the correct scopes to be able to return an access token. If the response says invalid scope please edit your api client in our dashboards:[ test environment](https://dashboard-test.idfy.io) / [prod environment](https://dashboard.idfy.io) or contact support@idfy.io

### Response

If your credentials are valid, the server will respond with a JSON body containing the access token and its expiration time:

```text
{
    "access_token": "xxxxx.yyyyy.zzzzz",
    "expires_in": 3600,
    "token_type": "Bearer"
}
```

## 2\) Use the obtained token

You can now store and use the access token to make authenticated request by passing it as an authentication header:

`Authorization: Bearer xxxxx.yyyyy.zzzzz`

