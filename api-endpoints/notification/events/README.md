# Events

Events are our way of letting you know when something happens in your account. For example, when a document is signed, we create a [`DocumentSigned`](./#documentsignedevent) event.

Events can be handled in multiple ways:

* [Webhooks](webhooks.md)
* [Events REST API](https://developer.idfy.io/api#tag/Events)
* [.NET Events Client](.net-events-client.md)

## Event format

All events share a common structure that includeds the necessary information to process the event. Note that the `payload` object will vary depending on the type of event. See [Event Types & Payloads](./#event-types--payloads) for a complete list of the various event payloads.

| Property | Type | Description |
| --- | --- | --- |
| `id` | `string` | Unique identifier for the event |
| `timestamp` | `string` | Time at which the event was created \(ISO 8601\) |
| `accountId` | `string` | Unique identifier for the Idfy account |
| `type` | `string` | The type of event that occured |
| `payload` | `object` | Unique object determined by the event type |

Example:

```javascript
{
  "id": "fce05bc5-0c13-42fd-96e2-bc51c8975eb1",
  "timestamp": "2017-10-30T09:00:00Z",
  "accountId": "e0e7e75e-d6ac-42bf-be4b-128ca29dfe4c",
  "type": "document_created",
  "payload": {
    "documentId": "8bfae710-5e4b-4464-ab7a-167f73c37590",
    "externalDocumentId": "8577545740"
  }
}
```

## Event Types & Payloads

Each event has a similar JSON schema, but will also contain a unique `payload` object with relevant event information.

* [DocumentBeforeDeletedEvent](./#documentbeforedeletedevent)
* [DocumentCanceledEvent](./#documentcanceledevent)
* [DocumentCreatedEvent](./#documentcreatedevent)
* [DocumentDeletedEvent](./#documentdeletedevent)
* [DocumentExpiredEvent](./#documentexpiredevent)
* [DocumentEmailOpenedEvent](./#documentemailopenedevent)
* [DocumentFormPartiallySignedEvent](./#documentformpartiallysignedevent)
* [DocumentFormSignedEvent](./#documentformsignedevent)
* [DocumentLinkOpenedEvent](./#documentlinkopenedevent)
* [DocumentPackagedEvent](./#documentpackagedevent)
* [DocumentPartiallySignedEvent](./#documentpartiallysignedevent)
* [DocumentReadEvent](./#documentreadevent)
* [DocumentSignedEvent](./#documentsignedevent)

### DocumentBeforeDeletedEvent

Triggered when a document is about to be deleted.

#### Payload

| key | type | description |
| :--- | :--- | :--- |
| `documentId` | `string` | A unique identifier for the document |
| `externalDocumentId` | `string` | The external identifier for the document |

#### Payload example

```javascript
{
  "documentId": "8bfae710-5e4b-4464-ab7a-167f73c37590",
  "externalDocumentId": "8577545740"
}
```

### DocumentCanceledEvent

Triggered when a document is canceled.

#### Payload

| key | type | description |
| :--- | :--- | :--- |
| `documentId` | `string` | A unique identifier for the document |
| `externalDocumentId` | `string` | The external identifier for the document |
| `message` | `string` | The message that was provided when canceling the document |

#### Payload example

```javascript
{
  "documentId": "8bfae710-5e4b-4464-ab7a-167f73c37590",
  "externalDocumentId": "8577545740",
  "message": "Canceled message"
}
```

### DocumentCreatedEvent

Triggered when a new document is created.

#### Payload

| key | type | description |
| :--- | :--- | :--- |
| `documentId` | `string` | A unique identifier for the document |
| `externalDocumentId` | `string` | The external identifier for the document |

#### Payload example

```javascript
{
  "documentId": "8bfae710-5e4b-4464-ab7a-167f73c37590",
  "externalDocumentId": "8577545740"
}
```

### DocumentDeletedEvent

Triggered when a document is deleted.

#### Payload

| key | type | description |
| :--- | :--- | :--- |
| `documentId` | `string` | A unique identifier for the document |
| `externalDocumentId` | `string` | The external identifier for the document |
| `message` | `string` | The message that was provided when deleting the document |

#### Payload example

```javascript
{
  "documentId": "8bfae710-5e4b-4464-ab7a-167f73c37590",
  "externalDocumentId": "8577545740",
  "message": "Deleted message"
}
```

### DocumentExpiredEvent

Triggered when a document expires.

#### Payload

| key | type | description |
| :--- | :--- | :--- |
| `documentId` | `string` | A unique identifier for the document |
| `externalDocumentId` | `string` | The external identifier for the document |

#### Payload example

```javascript
{
  "documentId": "8bfae710-5e4b-4464-ab7a-167f73c37590",
  "externalDocumentId": "8577545740"
}
```

### DocumentEmailOpenedEvent

Triggered when a signer opens a document email.

#### Payload

| key | type | description |
| :--- | :--- | :--- |
| `documentId` | `string` | A unique identifier for the document |
| `externalDocumentId` | `string` | The external identifier for the document |
| `email` | `string` | The email address of the signer |
| `signer` | `object` | Details about the signer |

#### Payload example

```javascript
{
  "documentId": "8bfae710-5e4b-4464-ab7a-167f73c37590",
  "externalDocumentId": "8577545740",
  "email": "john@doe.com",
  "signer": {
    "id": "954393cf-1086-4a2b-a98a-97e1feeded87",
    "externalSignerId": "GJNHS0UHAD"
  }
}
```

### DocumentFormPartiallySignedEvent

Triggered when a form is partially signed.

#### Payload

| key | type | description |
| :--- | :--- | :--- |
| `documentId` | `string` | A unique identifier for the document |
| `externalDocumentId` | `string` | The external identifier for the document |
| `schemaId` | `string` | A unique identifier for the form |
| `schema` | `string` | The name of the form |
| `formFields` | `object` | The names and values of the form's fields |
| `signer` | `object` | Details about the signer |

#### Payload example

```javascript
{
  "documentId": "8bfae710-5e4b-4464-ab7a-167f73c37590",
  "externalDocumentId": "8577545740",
  "schemaId": "f12d3961-3e9c-4094-b0ef-b4d01a54aeee",
  "schema": "Property declaration form",
  "formFields": {
    "company": "Affordable Housing Inc.",
    "address": "300 Main Street",
  },
  "signer": {
    "id": "954393cf-1086-4a2b-a98a-97e1feeded87",
    "fullName": "John Doe",
    "signedTime": "2017-03-01T13:00:00Z",
    "dateOfBirth": "1988-01-01",
    "externalSignerId": "GJNHS0UHAD",
    "signatureMethod": "no_bankid",
    "signatureMethodUniqueId": "9876-5000-4-32100"
  }
}
```

### DocumentFormSignedEvent

Triggered when a form is signed by all required signers.

#### Payload

| key | type | description |
| :--- | :--- | :--- |
| `documentId` | `string` | A unique identifier for the document |
| `externalDocumentId` | `string` | The external identifier for the document |
| `schemaId` | `string` | A unique identifier for the form |
| `schema` | `string` | The name of the form |
| `formFields` | `object` | The names and values of the form's fields |
| `signedTime` | `string` | A timestamp with the date and time the document was signed |
| `signers` | `array` | An array of signer objects with details about each signer |

#### Payload example

```javascript
{
  "documentId": "8bfae710-5e4b-4464-ab7a-167f73c37590",
  "externalDocumentId": "8577545740",
  "schemaId": "f12d3961-3e9c-4094-b0ef-b4d01a54aeee",
  "schema": "Property declaration form",
  "formFields": {
    "company": "Affordable Housing Inc.",
    "address": "300 Main Street",
  },
  "signedTime": "2017-03-01T13:00:00Z",
  "signers": [{
    "id": "954393cf-1086-4a2b-a98a-97e1feeded87",
    "fullName": "John Doe",
    "signedTime": "2017-03-01T13:00:00Z",
    "dateOfBirth": "1988-01-01",
    "externalSignerId": "GJNHS0UHAD",
    "signatureMethod": "no_bankid",
    "signatureMethodUniqueId": "9876-5000-4-32100"
  }]
}
```

### DocumentLinkOpenedEvent

Triggered when a document link is opened by a signer.

#### Payload

| key | type | description |
| :--- | :--- | :--- |
| `documentId` | `string` | A unique identifier for the document |
| `externalDocumentId` | `string` | The external identifier for the document |
| `userAgent` | `string` | The signers user agent |
| `ipAddress` | `string` | The signers IP address |
| `signer` | `object` | Details about the signer |

#### Payload example

```javascript
{
  "documentId": "8bfae710-5e4b-4464-ab7a-167f73c37590",
  "externalDocumentId": "8577545740",
  "userAgent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/63.0.3239.132 Safari/537.36",
  "ipAddress": "255.255.255.0",
  "signer": {
    "id": "954393cf-1086-4a2b-a98a-97e1feeded87",
    "externalSignerId": "GJNHS0UHAD"
  }
}
```

### DocumentPackagedEvent

Triggered when a document is packaged with all the signatures.

#### Payload

| key | type | description |
| :--- | :--- | :--- |
| `documentId` | `string` | A unique identifier for the document |
| `externalDocumentId` | `string` | The external identifier for the document |
| `downloadUrl` | `string` | URL to download the signed PAdES \(for .PDF documents only\) |
| `urlExpiresAt` | `string` | Time at which the download URL expires \(ISO 8601\) |
| `checksum` | `string` | SHA-256 checksum of the PAdES |

#### Payload example

```javascript
{
  "documentId": "8bfae710-5e4b-4464-ab7a-167f73c37590",
  "externalDocumentId": "8577545740"
}
```

### DocumentPartiallySignedEvent

Triggered when a document is signed by one of the signers.

#### Payload

| key | type | description |
| :--- | :--- | :--- |
| `documentId` | `string` | A unique identifier for the document |
| `externalDocumentId` | `string` | The external identifier for the document |
| `signer` | `object` | Details about the signer |

#### Payload example

```javascript
{
  "documentId": "8bfae710-5e4b-4464-ab7a-167f73c37590",
  "externalDocumentId": "8577545740",
  "signer": {
    "id": "954393cf-1086-4a2b-a98a-97e1feeded87",
    "fullName": "John Doe",
    "signedTime": "2017-03-01T13:00:00Z",
    "dateOfBirth": "1988-01-01",
    "externalSignerId": "GJNHS0UHAD",
    "signatureMethod": "no_bankid",
    "signatureMethodUniqueId": "9876-5000-4-32100"
  }
}
```

### DocumentReadEvent

Triggered when a document is read by one of the signers.

#### Payload

| key | type | description |
| :--- | :--- | :--- |
| `documentId` | `string` | A unique identifier for the document |
| `externalDocumentId` | `string` | The external identifier for the document |
| `userAgent` | `string` | The signers user agent |
| `ipAddress` | `string` | The signers IP address |
| `signer` | `object` | Details about the signer |

#### Payload example

```javascript
{
  "documentId": "8bfae710-5e4b-4464-ab7a-167f73c37590",
  "externalDocumentId": "8577545740",
  "userAgent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/63.0.3239.132 Safari/537.36",
  "ipAddress": "255.255.255.0",
  "signer": {
    "id": "954393cf-1086-4a2b-a98a-97e1feeded87",
    "externalSignerId": "GJNHS0UHAD"
  }
}
```

### DocumentSignedEvent

Triggered when a document is signed by all required signers.

#### Payload

| key | type | description |
| :--- | :--- | :--- |
| `documentId` | `string` | A unique identifier for the document |
| `externalDocumentId` | `string` | The external identifier for the document |
| `signedTime` | `string` | A timestamp with the date and time the document was signed |
| `signers` | `array` | An array of signer objects with details about each signer |

#### Payload example

```javascript
{
  "documentId": "8bfae710-5e4b-4464-ab7a-167f73c37590",
  "externalDocumentId": "8577545740",
  "signedTime": "2017-03-01T13:00:00Z",
  "signers": [{
    "id": "954393cf-1086-4a2b-a98a-97e1feeded87",
    "fullName": "John Doe",
    "signedTime": "2017-03-01T13:00:00Z",
    "dateOfBirth": "1988-01-01",
    "externalSignerId": "GJNHS0UHAD",
    "signatureMethod": "no_bankid",
    "signatureMethodUniqueId": "9876-5000-4-32100"
  }]
}
```

