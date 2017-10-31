# Events

Events are our way of letting you know when something happens in your account. For example, when a document is signed, we create a [`DocumentSigned`](#documentsignedevent) event.

Events can be handled in multiple ways:

* [Events REST API](https://event-test.idfy.io)
* [Webhooks](/webhooks.md)
* [.NET Events Client](https://github.com/idfy-io/Idfy.Events.Client)

## Event Types & Payloads

Each event has a similar JSON schema, but will also contain a unique `payload` object that represents any data associated with the event.

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
    "signerId": "954393cf-1086-4a2b-a98a-97e1feeded87",
    "signerName": "John Doe",
    "signedTime": "2017-03-01T13:00:00Z",
    "dateOfBirth": "1988-01-01",
    "signatureMethod": "no_bankid",
    "socialSecurityNumber": "01018812345"
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
    "signerId": "954393cf-1086-4a2b-a98a-97e1feeded87",
    "signerName": "John Doe",
    "signedTime": "2017-03-01T13:00:00Z",
    "dateOfBirth": "1988-01-01",
    "signatureMethod": "no_bankid",
    "socialSecurityNumber": "01018812345"
  }]
}
```



