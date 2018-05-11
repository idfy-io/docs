# Dealer

Idfy offers dealship to partners that implements Idfy solutions and product. bla bla

Advandtages of beeing a dealer:

* Create account automatically via the API, the dasboard 
* Via the dashboard you have full control over your customers accounts from logs, invoicing to api access.
* Choose to bill your customers your self or let Idfy bill your customers for you.

## Onboarding

Idfy have a automatic onboarding solution for that dealers also could use, below you can find the url parameters that you could use. You can get your dealerId from the Dashboard or from support@idfy.io.

**Site url : **[https://onboard.idfy.no/register](https://onboard.idfy.no/register)

The onboarding site can be used as is, with Idfy logo and description, or you can define the url with optional parameters to change the look of the onboarding solution. The form fields can be prefilled with these parameters, and the delivery of the user credentials can be set. See information below.

### Onboarding url with optional parameters

You can add these query parameters to the onboarding site url for extra functionality

| Parameter | Type | Possible values | Description |
| :--- | :--- | :--- | :--- |
| environment | string | prod, test, prodAndtest | Sets the signere environment the new customer will be granted \(default is test\) |
| dealer | GUID |  | If the dealerid exists, the site will be presented with the dealer logo and description text \(if defined\) |
| dealerref | string | Any | dealer reference |
| product | string | API | The product that the customer will be granted \(For now only API is available in the onboarding solution\) |
| lang | string | no, en, da, sv | Set the language of the page upon arrival |
| country | string | no, se, dk, fi, other | Set the organization country, combine with org number to autocomplete form |
| pushurl | string | Any valid pushurl | If defined the credentials will be pushed to this url as a signed jwt hook |
| orgnr | int |  | The orgnumber for the new customer. Combine this with country to autocomplete form. |
| contactperson | string |  | Name of the contactperson |
| mobilenr | string |  | The contactperson's mobile nr |
| email | string |  | The contactperson's email address |
| dealerhandlessign | boolean | 0, false, 1, true | If set to true, the dealer will have to create the user agreement and handle signing of this |
| returnurl | string | any valid url \(Must include http://, https://\) | Define this to redirect here after registration is complete |
| idproviders | string | nobank, buypass, swebank, nemid, tupas, mconnect | Choose which id providers the customer can choose between, separate by comma \(ex. [https://onboard.idfy.no/register?idproviders=nobank,swebank,mconnect](https://onboard.idfy.no/register?idproviders=nobank,swebank,mconnect) |
| includelegacy | boolean | 0, false, 1, true | Set this to true if you need the legacy api keys |

#### Onboarding webhook

**How to use push url / JWT webhook**

When a push url is added as a parameter in the onboarding url, the generated API keys will be delievered as a signed JWT to this address. If both prod and pre-prod environment is ordered they will be sent as two separate JWT messages.

Example result:

```javascript
{
      "Environment": "PreProd",
      "AccountId": "54f907ef-738e-4266-9af1-1dfac5f7948f",
      "DealerRef": "435678",  
      "MvaNumber": "123456789",         
      {
            "ClientId": "315daf91-45ae-47c2-89de-ebf9b46af894",
            "ClientSecret": "uandiuqn329oj2qm3dimdpamepodawdpa",
            "Scopes": ["identify", "document_read", "document_write"]
      }
}
```

**Info: Environment can have the value "Prod" and "PreProd"**

**Validate JWT**

For security reasons you have to check that the received JWT signature is valid. You can do this by sending a HTTP request to our API, we will then check that the signature is ours. If the JWT is valid we will return http status 200 \(ok\), if the signature is corrupted the return message is http status 400 \(Bad request\).

Address \(Http GET\)[https://onboard.idfy.io/api/jwt/verify?jwt=\[jwt\]](https://onboard.idfy.io/api/jwt/verify?jwt=[jwt]%28https://onboard.idfy.io/api/jwt/verify?jwt=[jwt%29]%28https://onboard.idfy.io/api/jwt/verify?jwt=[jwt]%28https://onboard.idfy.io/api/jwt/verify?jwt=[jwt%29%29]%28https://onboard.idfy.io/api/jwt/verify?jwt=[jwt]%28https://onboard.idfy.io/api/jwt/verify?jwt=[jwt%29]%28https://onboard.idfy.io/api/jwt/verify?jwt=[jwt]%28https://onboard.idfy.io/api/jwt/verify?jwt=[jwt%29%29%29]%28https://onboard.idfy.io/api/jwt/verify?jwt=[jwt]%28https://onboard.idfy.io/api/jwt/verify?jwt=[jwt%29]%28https://onboard.idfy.io/api/jwt/verify?jwt=[jwt]%28https://onboard.idfy.io/api/jwt/verify?jwt=[jwt%29%29]%28https://onboard.idfy.io/api/jwt/verify?jwt=[jwt]%28https://onboard.idfy.io/api/jwt/verify?jwt=[jwt%29]%28https://onboard.idfy.io/api/jwt/verify?jwt=[jwt]%28https://onboard.idfy.io/api/jwt/verify?jwt=[jwt%29%29%29%29]%28https://onboard.idfy.io/api/jwt/verify?jwt=[jwt]%28https://onboard.idfy.io/api/jwt/verify?jwt=[jwt%29]%28https://onboard.idfy.io/api/jwt/verify?jwt=[jwt]%28https://onboard.idfy.io/api/jwt/verify?jwt=[jwt%29%29]%28https://onboard.idfy.io/api/jwt/verify?jwt=[jwt]%28https://onboard.idfy.io/api/jwt/verify?jwt=[jwt%29]%28https://onboard.idfy.io/api/jwt/verify?jwt=[jwt]%28https://onboard.idfy.io/api/jwt/verify?jwt=[jwt%29%29%29]%28https://onboard.idfy.io/api/jwt/verify?jwt=[jwt]%28https://onboard.idfy.io/api/jwt/verify?jwt=[jwt%29]%28https://onboard.idfy.io/api/jwt/verify?jwt=[jwt]%28https://onboard.idfy.io/api/jwt/verify?jwt=[jwt%29%29]%28https://onboard.idfy.io/api/jwt/verify?jwt=[jwt]%28https://onboard.idfy.io/api/jwt/verify?jwt=[jwt%29]%28https://onboard.idfy.io/api/jwt/verify?jwt=[jwt]%28https://onboard.idfy.io/api/jwt/verify?jwt=[jwt%29%29%29%29%29\)

To become a dealer contact [sales@idfy.io](mailto:sales@idfy.io)

