# Webhooks

Webhooks allow you to subscribe to certain events on your Idfy account. When one of those events is triggered, we'll send a HTTP POST payload to the webhook's configured URL.

* [Webhook events](#webhook-events)
* [Event format](#event-format)
* [Creating webhooks](#creating-webhooks)
* [Required 2xx Success response](#required-2xx-success-response)
* [Securing your webhooks](#securing-your-webhooks)

## Webhook events

When configuring a webhook, you can choose which events you would like to subscribe to. The available events are listed below.

| Type | Description |
| :--- | :--- |
| [`document_canceled`](/events/#documentcanceledevent) | A document was canceled |
| [`document_created`](/events/#documentcreatedevent) | A new document has been created |
| [`document_deleted`](/events/#documentdeletedevent) | A document was deleted |
| [`document_expired`](/events/#documentexpiredevent) | A document has expired and can no longer be signed |
| [`document_packaged`](/events/#documentpartiallysignedevent) | A document was packaged with all signatures |
| [`document_partially_signed`](/events/documentpartiallysignedevent) | A document was partially signed |
| [`document_read`](/events/#documentreadevent) | A document was read by a signer |
| [`document_signed`](/events/#documentsignedevent) | A document was signed by all required signers |

### Wildcard event
We also support a wildcard (`*`) that will subscribe you to all events (including all new events in the future). 

Adding the wildcard event to an existing webhook will remove the existing specific events.

## Event format

All webhook events share a common structure that includeds the necessary information to process the event. Note that the `payload` object will vary depending on the type of event. See [Event Types & Payloads](/events/#event-types--payloads) for a complete list of the various event payloads.

| Property | Type | Description |
| --- | --- | --- |
| `id` | string | Unique identifier for the event |
| `timestamp` | string | Time at which the event was created \(ISO 8601\) |
| `type` | string | The type of event that occured |
| `payload` | object | Unique object determined by the event type |

Example:

```json
{
  "id": "fce05bc5-0c13-42fd-96e2-bc51c8975eb1",
  "timestamp": "2017-10-30T09:00:00Z",
  "type": "document_created",
  "payload": {
    "documentId": "8bfae710-5e4b-4464-ab7a-167f73c37590",
    "externalDocumentId": "8577545740"
  }
}
```

## Creating webhooks

Webhooks can be created and managed through the [Events API](http://event-test.idfy.io/#tag/Webhooks).

In the future you will also be able to manage webhooks directly from the Idfy Dashboard.

### Ping Event

When you create a new webhook, we'll send you a `ping` event to make sure your webhook endpoint is set up correctly. This event is not stored and can not be retrieved via the [Events API](http://event-test.idfy.io/#tag/Webhooks). A `ping` can also be triggered manually by using the [ping endpoint](http://event-test.idfy.io/#operation/Webhooks_PingWebhook).

## Required 2XX Success response

To acknowledge that you received the webhook without any problems, your server should return a `200 OK` HTTP status code. Any response code outside the 200 range will indicate that you did not receive the webhook.

Idfy expects a response within 10 seconds of sending the webhook event.

## Securing your webhooks

By default, a webhook endpoint is open and may receive a payload from anybody who knows the URL.  
For security reasons, we recommend you to ensure that the data is coming from Idfy. This can be done by setting up a secret token and use it to validate the payload.

### Creating your secret token



Coming soon.

### Validating payloads

Using your secret token, we create an HMAC-SHA256 signature of the request body. All requests include an `X-Idfy-Signature` containing this signature, which you then can use to validate the integrity of the payload and its origin.

To validate the request, compute the HMAC digest using your secret token as the signing key and ensure that it matches the signature from the header. Below is an example of how this can be done with Node.js:

```js
const crypto = require('crypto');
const secret = 'your-secret-token';

const payload = {
"message": "Hello, world"
};

const hmac = crypto.createHmac('sha256', secret);
const signature = hmac.update(JSON.stringify(payload)).digest('hex');
console.log(signature) // => def564b8df06ae55c788493cb414068b2cf017385d96ecb39aa3e844fdbbcdea
```



