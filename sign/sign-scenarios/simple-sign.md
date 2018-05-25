# Simple sign

A simple guide explaining how to sign a single document with one or more signers, no more fuzz.

> Step 1 - Get an api token
>
> Step 2 - Create request
>
> Step 3 - Read response
>
> Step 4 - Retrieve signed file

### Step 1 - Get an api token

First of all you need an API token, [**click here** ](/api-authentication.md)to see how you can retrieve it

### Step 2 - Create request

###### API-reference

```
https://developer.idfy.io/api#operation/Documents_Create
```

###### API-endpoint

```
 https://api.idfy.io/signature/documents 
```

###### Request

This simple request is all you need to get a document signed

```
{
  "title": "Test document",
  "description": "This is an important document",
  "externalId": "ae7b9ca7-3839-4e0d-a070-9f14bffbbf55",
  "dataToSign": {
    "base64Content": "VGhpcyB0ZXh0IGNhbiBzYWZlbHkgYmUgc2lnbmVk",
    "fileName": "sample.txt",
  },
  "contactDetails": {
    "email": "test@test.com",
    "url": "https://idfy.io"
  },
  "signers": [
    {
      "externalSignerId": "uoiahsd321982983jhrmnec2wsadm32",
      "redirectSettings": {
        "redirectMode": "donot_redirect"
      },
      "signatureType": {
        "mechanism": "pkisignature"
      },
    }
  ],
}
```

###### Things to consider

* Which redirect mode should I use? [Redirect settings and webmessages](/sign/events-redirect-settings-and-files/redirect-settings.md)
* [Signature formats](/sign/signature-formats-data-and-eid/signature-formats.md)

* [Data to sign](/sign/signature-formats-data-and-eid/data-to-sign.md "Data to sign format and more")

### Step 3



