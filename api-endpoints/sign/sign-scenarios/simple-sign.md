# Simple sign

A simple guide explaining how to sign a single document with one or more signers, no more fuzz.

> [Step 1 - Get an api token](simple-sign.md#step-1---get-an-api-token)
>
> [Step 2 - Create request](simple-sign.md#step-2---create-request)
>
> [Step 3 - Read response](simple-sign.md#step-3---read-response)
>
> [Step 4 - Retrieve signed file](simple-sign.md#step-4---retrieve-signed-file)
>
> [Optional - Include email / sms notifications](simple-sign.md#optional---include-email--sms-notifications)

## Step 1 - Get an api token

First of all you need an API token, [**click here** ](../../../api-authentication.md)to see how you can retrieve it

## Step 2 - Create request

#### API-reference

[https://developer.idfy.io/api\#operation/Documents\_Create](https://developer.idfy.io/api#operation/Documents_Create)

#### API-endpoint

```text
 [POST]
 https://api.idfy.io/signature/documents
```

#### Headers

| Key | Value |
| :--- | :--- |
| Authorization | Bearer "Your access token retrieved in step 1" |

#### Request

This simple request is all you need to get a document signed

```text
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

#### Things to consider

* [Redirect settings and webmessages](../events-redirect-settings-and-files/redirect-settings-and-webmessages.md)
* [Signature formats](../signature-formats-data-and-eid/signature-formats.md)
* [Data to sign](../signature-formats-data-and-eid/data-to-sign.md)

## Step 3 - Read response

The response you retrieve will look something like this

```text
{
    "documentId": "60474622-0f66-48de-b0ea-a8eb007cf5dd",
    "signers": [
        {
            "id": "32b23d9c-3549-4c45-a9bb-a8eb007cf657",
            "url": "https://sign-test.idfy.io/start?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzM4NCJ9.eyJrdmVyc2lvbiI6IjdmNzhjNzNkMmQ1MjQzZWRiYjdiNDI0MmI2MDE1MWU4IiwiZG9jaWQiOiI2MDQ3NDYyMi0wZjY2LTQ4ZGUtYjBlYS1hOGViMDA3Y2Y1ZGQiLCJhaWQiOiJkNjJhODZjZi04N2FkLTQwYTgtOTExMy1hMjg5MDA3MTk2ODYiLCJsZyI6bnVsbCwiZXJyIjpudWxsLCJpZnIiOmZhbHNlLCJ3Ym1zZyI6ZmFsc2UsInNmaWQiOiIzMmIyM2Q5Yy0zNTQ5LTRjNDUtYTliYi1hOGViMDA3Y2Y2NTciLCJ1cmxleHAiOm51bGwsImF0aCI6bnVsbCwiZHQiOiJUZXN0IGRvY3VtZW50IiwidmYiOmZhbHNlLCJhbiI6IkJhbmtJRCBtb2JpbCB0ZXN0IiwidGgiOiIiLCJzcCI6bnVsbCwiZG9tIjpudWxsLCJyZGlyIjpmYWxzZSwidXQiOiJ3ZWIiLCJ1dHYiOm51bGwsInNtIjoidGVzdEB0ZXN0LmNvbSJ9.GbmEevZILyRqHySZUwqs13BSuCWFJ9KSE_dRYM-ucU_y6VcbibtSvDdNUTNy7LJi",
            "links": [],
            "externalSignerId": "uoiahsd321982983jhrmnec2wsadm32",
            "redirectSettings": {
                "redirectMode": "donot_redirect"
            },
            "signatureType": {
                "mechanism": "pkisignature",
                "onEacceptUseHandWrittenSignature": false
            },
            "tags": [],
            "order": 0,
            "required": false
        }
    ],
    "status": {
        "documentStatus": "unsigned",
        "completedPackages": [],
        "attachmentPackages": {}
    },
    "title": "Test document",
    "description": "This is an important document",
    "externalId": "ae7b9ca7-3839-4e0d-a070-9f14bffbbf55",
    "dataToSign": {
        "fileName": "sample.txt",
        "convertToPDF": false
    },
    "contactDetails": {
        "email": "test@test.com",
        "url": "https://idfy.io"
    }
}
```

As you can see an url is included in the signer object, this is where the signer needs to be redirectet to.

## Step 4 - Retrieve signed file

When the document is signed and ready it is time to retrieve the signed document.

### [Click here to read about file retrieval](../events-redirect-settings-and-files/files.md)

## Optional - Include email / sms notifications

We can handle the email / sms notifications regarding this document for you, [read more here](../styling-and-notifications/email-sms.md)

