# Webhooks

Webhooks allow you to subscribe to certain events on your Idfy account. When one of those events is triggered, we'll send a HTTP POST payload to the webhook's configured URL.

* [Webhook events](#webhook-events)
* [Event format](#event-format)
* [Creating webhooks](#creating-webhooks)
* [Required 200 OK response](#required-2xx-success-response)
* [Securing your webhooks](#securing-your-webhooks)

## Webhook events

When configuring a webhook, you can choose which events you would like to subscribe to. The available events are listed below.

| Type | Description |
| :--- | :--- |
| [`document_canceled`](/events.md#documentcanceledevent) | A document was canceled |
| [`document_created`](/events.md#documentcreatedevent) | A new document has been created |
| [`document_deleted`](/events.md#documentdeletedevent) | A document was deleted |
| [`document_expired`](/events.md#documentexpiredevent) | A document has expired and can no longer be signed |
| [`document_packaged`](/events.md#documentpartiallysignedevent) | A document was packaged with all signatures |
| [`document_partially_signed`](/events.md#documentpartiallysignedevent) | A document was partially signed |
| [`document_read`](/events.md#documentreadevent) | A document was read by a signer |
| [`document_signed`](/events.md#documentsignedevent) | A document was signed by all required signers |

## Event format

All webhook events share a common structure that includeds the necessary information to process the event. Note that the `payload` object will vary depending on the type of event. See [Event Types & Payloads](/events.md#event-types--payloads) for a complete list of the various event payloads.

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

To create a webhook, simply specify the URL to the endpoint on your server when creating a new document. This is done by setting the `advanced.webhook` property in the body of the `POST api/documents` request:

```json
{
  "advanced": {
    "webhook": "https://example.com/webhook-endpoint"
  }
}
```

In the future you will also be able to manage webhooks directly from the Idfy Dashboard.

## Required 2XX Success Response

To acknowledge that you received the webhook without any problems, your server should return a `200 OK` HTTP status code. Any response code outside the 200 range will indicate that you did not receive the webhook.

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



