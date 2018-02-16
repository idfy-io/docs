# Events

Events are our way of letting you know when something happens in your account. For example, when a document is signed, we create a [`DocumentSigned`](#documentsignedevent) event.

Events can be handled in multiple ways:

* [Events REST API](https://event-test.idfy.io)
* [Webhooks](/events/webhooks.md)
* [.NET Events Client](/events/net-events-client.md)

## Event Types & Payloads

Each event has a similar JSON schema, but will also contain a unique `payload` object with relevant event information.

* [DocumentCanceledEvent](#documentcanceledevent)
* [DocumentCreatedEvent](#documentcreatedevent)
* [DocumentDeletedEvent](#documentdeletedevent)
* [DocumentExpiredEvent](#documentexpiredevent)
* [DocumentPackagedEvent](#documentpackagedevent)
* [DocumentPartiallySignedEvent](#documentpartiallysignedevent)
* [DocumentReadEvent](#documentreadevent)
* [DocumentSignedEvent](#documentsignedevent)

### DocumentCanceledEvent

Triggered when a document is canceled.

#### Payload

| key | type | description |
| :--- | :--- | :--- |
| `documentId` | `string` | A unique identifier for the document |
| `externalDocumentId` | `string` | The external identifier for the document |
| `message` | `string` | The message that was provided when canceling the document |

#### Payload example

```json
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

```json
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

```json
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

```json
{
  "documentId": "8bfae710-5e4b-4464-ab7a-167f73c37590",
  "externalDocumentId": "8577545740"
}
```

### DocumentPackagedEvent

Triggered when a document is packaged with all the signatures.

#### Payload

| key | type | description |
| :--- | :--- | :--- |
| `documentId` | `string` | A unique identifier for the document |
| `externalDocumentId` | `string` | The external identifier for the document |

#### Payload example

```json
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

```json
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
| `signerId` | `string` | A unique identifier for the signer |
| `userAgent` | `string` | The signers user agent |
| `ipAddress` | `string` | The signers IP address |

#### Payload example

```json
{
  "documentId": "8bfae710-5e4b-4464-ab7a-167f73c37590",
  "externalDocumentId": "8577545740"
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

```json
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



