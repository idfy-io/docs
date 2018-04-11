# Dealer

Idfy offers dealship to partners that implements Idfy solutions and product. bla bla

Advandtages of beeing a dealer:

* Create account automatically via the API, the dasboard 
* Via the dashboard you have full control over your customers accounts from logs, invoicing to api access.
* Choose to bill your customers your self or let Idfy bill your customers for you.

## Onboarding

Idfy have a automatic onboarding solution for that dealers also could use, below you can find the url parameters that you could use.
You can get your dealerId from the Dashboard or from support@idfy.io.

##### Site url : https://onboard.idfy.no/register

The onboarding site can be used as is, with Idfy logo and description, or you can define the url with optional parameters to change the look of the onboarding solution. The form fields can be prefilled with these parameters, and the delivery of the user credentials can be set. See information below.  


### Onboarding url with optional parameters

https://onboard.idfy.no/register?environment=[env]&dealer=[dealer]&dealerref=[dealerref]&product=[product]&lang=[lang]&pushurl=[url]&orgnr=[orgnr]&contactperson=[contactperson]&mobilenr=[mobilenr]&email=[email]&createevent=[createevent]&dealerhandlessign=[dealerhandlessign]&returnurl=[returnurl]

<table>
<tr>
<th>Parameter</th>
<th>Type</th>
<th>Possible values</th>
<th>Description</th>
</tr>
<tr><td>environment</td><td>string</td><td>prod, test, prodAndtest</td><td>Sets the signere environment the new customer will be granted (default is test)</td> </tr>
<tr><td>dealer</td><td>GUID</td><td></td><td>If the dealerid exists, the site will be presented with the dealer logo and description text (if defined) </td> </tr>
<tr><td>dealerref</td><td>string</td><td>Any</td><td>dealer reference</td> </tr>
<tr><td>product</td><td>string</td><td>API</td><td>The product that the customer will be granted (For now only API is available in the onboarding solution)</td> </tr>
<tr><td>lang</td><td>string</td><td>no, en</td><td>Set the language of the page upon arrival</td></tr>
<tr><td>pushurl</td><td>string</td><td>Any valid pushurl</td><td>If defined the credentials will be pushed to this url as a signed jwt hook</td></tr>
<tr><td>orgnr</td><td>int</td><td></td><td>The orgnumber for the new customer</td></tr>
<tr><td>contactperson</td><td>string</td><td></td><td>Name of the contactperson</td></tr>
<tr><td>mobilenr</td><td>string</td><td></td><td>The contactperson's mobile nr</td></tr>
<tr><td>email</td><td>string</td><td></td><td>The contactperson's email address</td></tr>
<tr><td>createevent</td><td>boolean</td><td>0, false, 1, true</td><td>If set to true, a rebusqueue event connectionstring will be added and provided with the API keys</td></tr>
<tr><td>dealerhandlessign</td><td>boolean</td><td>0, false, 1, true</td><td>If set to true, the dealer will have to create the user agreement and handle signing of this</td></tr>
<tr><td>returnurl</td><td>string</td><td>any valid url (Must include http://, https://)</td><td>Define this to redirect here after registration is complete</td></tr>
<tr><td>idproviders</td><td>string</td><td>nobank,buypass,swebank,nemid,tupas,mconnect</td><td>Choose which id providers the customer can choose between, separate by comma (ex. <a href="https://onboard.idfy.no/register?idproviders=nobank,swebank,mconnect" target="_blank">https://onboard.idfy.no/register?idproviders=nobank,swebank,mconnect</a></td></tr>
</table>

#### Onboarding webhook

##### How to use push url / JWT webhook

When a push url is added as a parameter in the onboarding url, the generated API keys will be delievered as a signed JWT to this address. If both prod and pre-prod environment is ordered they will be sent as two separate JWT messages. 

Example result:

```json
{
      "Environment": "PreProd",
      "AccountId": "54f907ef-738e-4266-9af1-1dfac5f7948f",
      "DealerRef": "435678",  
      "MvaNumber": "123456789",     
      "EventConnectionString":       "Endpoint=sb://signerelocaleventtest.servicebus.windows.net/;SharedAccessKeyName=6dfgrehgrythytrjnfdghrfyujht;SharedAccessKey=dfgjh6ytujtjuythjdujyrytkdsafgte="
      "OauthCredentials": 
      {
            "ClientId": "315daf91-45ae-47c2-89de-ebf9b46af894",
            "ClientSecret": "uandiuqn329oj2qm3dimdpamepodawdpa",
            "Scopes": ["identify", "document_read", "document_write"]
      }
}

```


##### Info: Environment can have the value "Prod" and "PreProd"

##### Validate JWT

For security reasons you have to check that the received JWT signature is valid. You can do this by sending a HTTP request to our API, we will then check that the signature is ours. If the JWT is valid we will return http status 200 (ok), if the signature is corrupted the return message is http status 400 (Bad request). 

Address (Http GET)
https://onboard.idfy.io/api/jwt/verify?jwt=[jwt]
***


To become a dealer contact [sales@idfy.io](mailto:sales@idfy.io)

