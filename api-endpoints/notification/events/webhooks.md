# Webhooks

Webhooks allow you to subscribe to certain events on your Idfy account. When one of those events is triggered, we'll send a HTTP POST payload to the webhook's configured URL.

* [Webhook events](webhooks.md#webhook-events)
* [Creating webhooks](webhooks.md#creating-webhooks)
* [Required 2xx Success response](webhooks.md#required-2xx-success-response)
* [Securing your webhooks](webhooks.md#securing-your-webhooks)

## Webhook events

When configuring a webhook, you can choose which events you would like to subscribe to. The available events are listed below.

| Type | Description |
| :--- | :--- |
| [`document_before_deleted`](./#documentbeforedeletedevent) | A document is about to be deleted |
| [`document_canceled`](./#documentcanceledevent) | A document was canceled |
| [`document_created`](./#documentcreatedevent) | A new document has been created |
| [`document_deleted`](./#documentdeletedevent) | A document was deleted |
| [`document_expired`](./#documentexpiredevent) | A document has expired and can no longer be signed |
| [`document_email_opened`](./#documentemailopenedevent) | A signer opened a document email |
| [`document_form_partially_signed`](./#documentformpartiallysignedevent) | A form was partially signed |
| [`document_form_signed`](./#documentformsignedevent) | A form was signed by all required signers |
| [`document_link_opened`](./#documentlinkopenedevent) | A document link was opened by a signer |
| [`document_packaged`](./#documentpackagedevent) | A document was packaged with all signatures |
| [`document_partially_signed`](./#documentpartiallysignedevent) | A document was partially signed |
| [`document_read`](./#documentreadevent) | A document was read by a signer |
| [`document_signed`](./#documentsignedevent) | A document was signed by all required signers |

### Wildcard event

We also support a wildcard \(`*`\) that will subscribe you to all events \(including all new events in the future\).

Adding the wildcard event to an existing webhook will remove the existing specific events.

## Creating webhooks

Webhooks can be created and managed through our [REST API](https://developer.idfy.io/api#tag/Webhooks), or directly from the [Idfy Dashboard](https://dashboard.idfy.io).

### Ping Event

When you create a new webhook, we'll send you a `ping` event to make sure your webhook endpoint is set up correctly. This event is not stored and can not be retrieved via the [Events API](http://event-test.idfy.io/#tag/Webhooks). A `ping` can also be triggered manually by using the [ping endpoint](http://event-test.idfy.io/#operation/Webhooks_PingWebhook), or directly from the Idfy Dashboard.

## Required 2XX Success response

To acknowledge that you received the webhook without any problems, your server should return a `200 OK` HTTP status code. Any response code outside the 200 range will indicate that you did not receive the webhook.

Idfy expects a response within 10 seconds of sending the webhook event.

## Securing your webhooks

By default, a webhook endpoint is open and may receive a payload from anybody who knows the URL.  
For security reasons, we recommend you to ensure that the data is coming from Idfy. This can be done by setting up a secret token and use it to validate the payload.

### Creating your secret token

A secret token can be added to your webhook from the Idfy Dashboard or through the [Events API](http://event-test.idfy.io/#tag/Webhooks).  
It is recommended that you use a random string with high entropy.

### Validating payloads

Using your secret token, we create an HMAC-SHA256 signature of the request body. All requests include an `X-Idfy-Signature` header containing this signature, which you then can use to validate the integrity of the payload and its origin.

To validate the request, compute the HMAC digest using your secret token as the signing key and ensure that it matches the signature from the header. Below is an example of how this can be done with Node.js:

```javascript
const crypto = require('crypto');
const secret = 'your-secret-token';

const payload = {
  "message": "Hello, world"
};

const hmac = crypto.createHmac('sha256', secret);
const signature = hmac.update(JSON.stringify(payload)).digest('hex');
console.log(signature) // => def564b8df06ae55c788493cb414068b2cf017385d96ecb39aa3e844fdbbcdea
```

