# Files

API reference: [https://developer.idfy.io/api\#tag/Files](https://developer.idfy.io/api#tag/Files)

We only store signed files for a limited time, therefore you have to make sure to download them as soon as they are signed.

### File formats

You can read more about the different file formats available here: [Signature formats](/signature/signature-formats.md)

### When is the signed file ready?

##### Option 1:

Use our [Notification](/notification/README.md "Notification")[ ](/events/README.md)API to be notified when the document is packaged

* API reference: [https://developer.idfy.io/api\#tag/Notification-Endpoint](https://developer.idfy.io/api#tag/Notification-Endpoint)

##### Option 2:

Check if the document is ready by calling the document status endpoint. In the response you will se all the completed packages and if the document is signed.

* API reference: [https://developer.idfy.io/api\#operation/Documents\_Status](https://developer.idfy.io/api#operation/Documents_Status)

### Retrieve file

This endpoint delivers the main document file containing all the signatures.You can retrieve a file by specifying document id and which filetype you want.

###### Example

A signature job is completed, the file to be signed was a pdf, therefore we want to fetch the pades file:

```
Run http Get

 https://api.idfy.io/signature/files/documents/f7e5b94e-159a-42a9-9e07-33515db61a46?fileType=pades
```

### Retrieve file for signer

This endpoint can return the signed file for each signer \(native or packaged\) before they are merged together to one file

### Retrieve attachment file and attachment file for signer

Works the same way as Retrieve file, only for attachments

