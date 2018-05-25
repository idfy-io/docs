# Sign multiple documents

A guide explaining how to present multiple documents to the signer

> Step 1 - Get an api token
>
> Step 2 - Create request
>
> Step 3 - Upload attachments
>
> Step 4 - Read response
>
> Step 5 - Retrieve signed file
>
> Optional - Include email / sms notifications

### Step 1 - Get an api token

First of all you need an API token, [**click here** ](/api-authentication.md)to see how you can retrieve it

### Step 2 - Create request

First you have to create the document

###### API-reference

[https://developer.idfy.io/api\#operation/Documents\_Create](https://developer.idfy.io/api#operation/Documents_Create "Check out the API reference")

###### API-endpoint

```
 [POST]
 https://api.idfy.io/signature/documents
```

###### Headers

| Key | Value |
| :--- | :--- |
| Authorization | Bearer "Your access token retrieved in step 1" |

###### 

###### Request

This is an example of what the request can look like. **Notice how we have added the advanced object with "atttachments": 2. **This way we tell the document that we will upload two more documents in addition to the main document. When you include attachments here, the document job will wait until all the attachments are uploaded before anyone is allowed to sign or notifications are sent out.

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
  "advanced": {    
    "attachments": 2
  }
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

* [Redirect settings and webmessages](/sign/events-redirect-settings-and-files/redirect-settings.md)
* [Signature formats](/sign/signature-formats-data-and-eid/signature-formats.md)

* [Data to sign](/sign/signature-formats-data-and-eid/data-to-sign.md "Data to sign format and more")

### Step 3 - Upload attachments

###### API-reference

[https://developer.idfy.io/api\#operation/Attachments\_Create](https://developer.idfy.io/api#operation/Attachments_Create)

###### API-endpoint

Include the document id you retrieve in step one as a path parameter.

```
 [POST]
 https://api.idfy.io/signature/documents/{documentId}/attachments
```

###### Headers

| Key | Value |
| :--- | :--- |
| Authorization | Bearer "Your access token retrieved in step 1" |

**Example attachment request**

```text
{

    "fileName": "Attachment1.pdf",
    "title": "Attachment 1 - Type description",
    "data": "Base 64 encoded pdf",
    "description": "This attachment describes bla bla bla...",
    "type": "show_accept",
    "signers": null

}
```

###### Requirements:

* The fileName must include the .pdf extension
* The data property must be a base64 encoded valid pdf

###### **Hint:**

If you only want some of the signers to retrieve an attachment; specify which in the signers property which is sat to null in the example above. The data type is a list with the signer id's you want to include.

#### [Read more about attachments here](/sign/attachments-and-dialogs/attachments.md)

#### 

### Step 3 - Result

When all the attachments are uploaded the document job will continue it's work and the document can be signed

### Step 4 - Read response you retrieved in step 2

The response you retrieve will look something like this

```
{
    "documentId": "9bdb48c9-1123-49d5-a91b-a8eb0099bc48",
    "signers": [
        {
            "id": "6070e7ff-db6b-4141-9324-a8eb0099bc6b",
            "url": "https://sign-test.idfy.io/start?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzM4NCJ9.eyJrdmVyc2lvbiI6IjdmNzhjNzNkMmQ1MjQzZWRiYjdiNDI0MmI2MDE1MWU4IiwiZG9jaWQiOiI5YmRiNDhjOS0xMTIzLTQ5ZDUtYTkxYi1hOGViMDA5OWJjNDgiLCJhaWQiOiJkNjJhODZjZi04N2FkLTQwYTgtOTExMy1hMjg5MDA3MTk2ODYiLCJsZyI6bnVsbCwiZXJyIjpudWxsLCJpZnIiOmZhbHNlLCJ3Ym1zZyI6ZmFsc2UsInNmaWQiOiI2MDcwZTdmZi1kYjZiLTQxNDEtOTMyNC1hOGViMDA5OWJjNmIiLCJ1cmxleHAiOm51bGwsImF0aCI6bnVsbCwiZHQiOiJUZXN0IGRvY3VtZW50IiwidmYiOmZhbHNlLCJhbiI6IkJhbmtJRCBtb2JpbCB0ZXN0IiwidGgiOiIiLCJzcCI6bnVsbCwiZG9tIjpudWxsLCJyZGlyIjpmYWxzZSwidXQiOiJ3ZWIiLCJ1dHYiOm51bGwsInNtIjoidGVzdEB0ZXN0LmNvbSJ9.DPBcJkasry7UN-ad7yw6vwv5lsWnfybJ9q6LwX4L5fIksL1Kv-WRhV4bYKE793l6",
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
        "documentStatus": "waiting_for_attachments",
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
    },
    "advanced": {
        "attachments": 2,
        "requiredSignatures": 0,
        "getSocialSecurityNumber": false
    }
}
```

As you can see an url is included in the signer object, this is where the signer needs to be redirectet to.

### Step 5 - Retrieve signed file

When the document is signed and ready it is time to retrieve the signed document.

#### [Click here to read about file retrieval](/sign/events-redirect-settings-and-files/files.md)

### Optional - Include email / sms notifications

We can handle the email / sms notifications regarding this document for you, [read more here](/sign/styling-and-notifications/notifications.md)

