# Digital signatures quickstart

Securely collect digital signatures from your customers for your contracts and agreements, onboarding forms, declarations and more, using Nordic eIDs as mechanisms to sign with for your end users.

**Step 1:**

First, you need to establish a test account and API credentials. You can get a free API account in Idfy test environments by completing our onboarding form here: [https://onboard.idfy.io](https://onboard.idfy.io) and specifying that you want access to our signature services. You will then receive an e-mail with your API credentials, as well as some more information, test users and code examples.

**Step 2:**

When you have received your API credentials, you can use these to make calls towards the Idfy signature APIs. You can either make pure REST calls towards our APIs \(i.e. make your own HTTP client\), or use one of our pre-built SDKs in your preferred programming language. Check out our [SDKs](https://developer.idfy.io/sdk) and choose the SDK or approach that fits your needs best. One benefit of using an SDK is that you don't have to manage the API authentication and wrapping of HTTP calls yourself.

**Step 3:**

To get quickly started with testing the signature services, you can start using your preferred SDK and calling the appropriate methods within that given library, or you can for instance make some initial calls using cURL or the API tool Postman \(see more information and download Postman [here](https://www.getpostman.com/)\). For the sake of simplicity, we here show some initial calls using Postman. The Postman collection for the APIs can be found on our [SDK site](https://developer.idfy.io/sdk) \(click "Export", then "Postman 1.0" or "Postman 2.0"\). When you have downloaded this JSON file, open Postman and import the file as a collection.

**Step 4:**

Open Postman and the Idfy API reference collection. Browse to Documents, and "Documents\_Create". The parameters that are required for a minimal test follow below, with some example values that you can try, by pasting the JSON into the body of the request in Postman \(replace the example values that come from the collection\):

JSON:

```
{
    "signers":[
        {
            "externalSignerId":"123abc",
            "redirectSettings":{
                "redirectMode":"redirect",
                "success":"https://www.idfy.io#success",
                "abort":"https://www.idfy.io#abort",
                "error":"https://www.idfy.io#error"
            },
            "signatureType":{
                "signatureMethods":["NO_BANKID"],
                "mechanism":"pkisignature"
            }
        }
    ],
    "title":"Signature test",
    "description":"A small text to sign",
    "contactDetails":{
        "email":"support@idfy.io"
    },
    "dataToSign":{
        "fileName":"shortText.txt",
        "base64Content":"SGVsbG8gd29ybGQhIFNpZ24gdGhpcyBzaG9ydCB0ZXh0IHRvIHRyeSBvdXQgSWRmeSBBUElzLg=="
    },
    "externalId":"document-42"
}
```

Explanation of parameters:

| Parameters | Example value | Explanation |
| :--- | :--- | :--- |
| signers \(array - see below\) | \(array of values, see below\) | These are the individual signers that are to sign the document |
| signers\[0\].externalSignerId | "123abc" | Your own reference for the person to sign the document. Could e.g. be the customer number |
| signers.\[0\].redirectSettings.redirectMode | "redirect" | Determines how the signing application should behave for the user, e.g. if you are planning on redirecting the user to the signing URL, or if you are planning to iframe the signing process into your webpage. |
| signers\[0\].redirectSettings.success | "[https://www.idfy.io\#success](https://www.idfy.io#success)" | The landing page on your end, where you want the user to be redirected after successful signature |
| signers\[0\].redirectSettings.abort | "[https://www.idfy.io\#abort](https://www.idfy.io#abort)" | The landing page on your end, where you want the user to be redirected if he/she chooses to abort the signing process |
| signers\[0\].redirectSettings.error | "[https://www.idfy.io\#error](https://www.idfy.io#error)" | The landing page on your end, where you want the user to be redirected in case any errors occur during the signing process |
| signers\[0\].signatureType.signatureMethods | \["NO\_BANKID"\] | The method for the user to sign with. Could be |
| signers\[0\].signatureType.method | "pkisignature" | Determines which type of signature is to be used. pkisignature means that the native signature capability of the signature method is to be used. |
| title | "Signature test" | This is the title of the document, which is shown in the GUI for the signer |
| description | "A small test text to sign" | This is the description for the document to sign, which is shown in the GUI for the signer |
| dataToSign.fileName | "shortText.txt" | This is the file name for the document that is sent for signing. Note that the correct extension for the document must be provided, e.g. .txt for text signing, and .pdf for PDF documents. |
| dataToSign.base64Content | "SGVsbG8gd29ybGQhIFNpZ24gdGhpcyBzaG9ydCB0ZXh0IHRvIHRyeSBvdXQgSWRmeSBBUElzLg==" | This is the base64 encoded file contents of the document to sign. The example value corresponds to the text "Hello world! Sign this short text to try out Idfy APIs." |
| externalId | "document-42" | This is your reference for the document to be signed. Could e.g. be your own internal documentID in your system |

Postman:

![](/assets/postman-sign-5.png)

**Step 5:**

When we have inserted the example body in Postman, we are almost ready for making an example call, but we need to get an authentication token so that the API recognizes us as a valid client. Postman handles OAuth2 for us, so we browse to the Authorization tab, and press "Get access token". Now we input the credentials that we got in step 1, using the client\_credentials grant type, "root" scope and the appropriate authorization URL for the test environment:

![](/assets/postman_sign3.png)

When we have got our access token above, we add it to the headers of the request, and press "Send":

![](/assets/postman_sign4.png)

In the response you should for each of the signers get a URL for the signer to use. Note that this URL by default is only valid for 7 days, but can be controlled via parameter settings:

![](/assets/postman-sign-6.png)

**Step 6:**

Enter the URL received in the response object \(under signers\[0\].url\). Since we specified redirect mode in step 4, the API assumes a full page mode in the GUI:

\[insert screenshot\]



You can also test right away how this plays out in Node:

Runkit

