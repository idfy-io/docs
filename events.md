# Events

An event has two properties: `type` and `payload`. Only `type` is required, but any data associated with the event is added to the `payload` object.

Example:

```json
{
  "type": "language_changed",
  "payload": {
    "language": "EN"
  }
}
```

## Webhooks
| Type        | Description     | 
| ------------- |:-------------:|
| [`document_canceled`](https://github.com/Signereno/signature/wiki/Events#documentcanceledevent) | A document was canceled |
| [`document_created`](https://github.com/Signereno/signature/wiki/Events#documentcreatedevent) | A new document has been created |
| [`document_deleted`](https://github.com/Signereno/signature/wiki/Events#documentdeletedevent) | A document was deleted | 
| [`document_expired`](https://github.com/Signereno/signature/wiki/Events#documentexpiredevent) | A document has expired and can no longer be signed  |
| [`document_partially_signed`](https://github.com/Signereno/signature/wiki/Events#documentpartiallysignedevent) | A document was partially signed |
| [`document_read`](https://github.com/Signereno/signature/wiki/Events#documentreadevent) | A document was read by a signer |
| [`document_signed`](https://github.com/Signereno/signature/wiki/Events#documentsignedevent) | A document was signed by all required signers

## Web Messages

| Type        | Description     | 
| ------------- |:-------------:|
| [`document_expired`](https://github.com/Signereno/signature/wiki/Events#documentexpiredevent) | The document has expired and can no longer be signed  |
| [`document_read`](https://github.com/Signereno/signature/wiki/Events#documentreadevent) | The document was read by the user |
| [`eid_selected`](https://github.com/Signereno/signature/wiki/Events#eidselectedevent) | User selected eID provider |
| [`language_changed`](https://github.com/Signereno/signature/wiki/Events#languagechangedevent) | User changed the app language |
| `sign_success` | The signature process was completed successfully |
| [`sign_error`](https://github.com/Signereno/signature/wiki/Events#signerrorevent) | The signature process could not be completed due to an error |
| `spinner_on` | The loading spinner is being shown to user |
| `spinner_off` | The loading spinner is no longer being shown to user |
| `user_aborted` | User aborted the signing process |

## Event Types & Payloads

### DocumentCanceledEvent

#### Payload

| key        | type     | description |
| ------------- |:-------------:|:-------------:|
| `documentId` | `string` | A unique identifier for the document
| `externalDocumentId` | `string` | The external identifier for the document
| `message` | `string` | The message that was provided when canceling the document

#### Payload example

```json
{
  "documentId": "8bfae710-5e4b-4464-ab7a-167f73c37590",
  "externalDocumentId": "8577545740",
  "message": "Canceled message"
}
```

### DocumentCreatedEvent

#### Payload

| key        | type     | description |
| ------------- |:-------------:|:-------------:|
| `documentId` | `string` | A unique identifier for the document
| `externalDocumentId` | `string` | The external identifier for the document

#### Payload example

```json
{
  "documentId": "8bfae710-5e4b-4464-ab7a-167f73c37590",
  "externalDocumentId": "8577545740"
}
```

### DocumentDeletedEvent

#### Payload

| key        | type     | description |
| ------------- |:-------------:|:-------------:|
| `documentId` | `string` | A unique identifier for the document
| `externalDocumentId` | `string` | The external identifier for the document
| `message` | `string` | The message that was provided when deleting the document

#### Payload example

```json
{
  "documentId": "8bfae710-5e4b-4464-ab7a-167f73c37590",
  "externalDocumentId": "8577545740",
  "message": "Deleted message"
}
```

### DocumentExpiredEvent

#### Payload

| key        | type     | description |
| ------------- |:-------------:|:-------------:|
| `documentId` | `string` | A unique identifier for the document
| `externalDocumentId` | `string` | The external identifier for the document

#### Payload example

```json
{
  "documentId": "8bfae710-5e4b-4464-ab7a-167f73c37590",
  "externalDocumentId": "8577545740"
}
```

### DocumentPartiallySignedEvent

#### Payload

| key        | type     | description |
| ------------- |:-------------:|:-------------:|
| `documentId` | `string` | A unique identifier for the document
| `externalDocumentId` | `string` | The external identifier for the document
| `signer` | `object` | Details about the signer

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

#### Payload

| key        | type     | description |
| ------------- |:-------------:|:-------------:|
| `documentId` | `string` | A unique identifier for the document
| `externalDocumentId` | `string` | The external identifier for the document

#### Payload example

```json
{
  "documentId": "8bfae710-5e4b-4464-ab7a-167f73c37590",
  "externalDocumentId": "8577545740"
}
```

### DocumentSignedEvent

#### Payload

| key        | type     | description |
| ------------- |:-------------:|:-------------:|
| `documentId` | `string` | A unique identifier for the document
| `externalDocumentId` | `string` | The external identifier for the document
| `signedTime` | `string` | A timestamp with the date and time the document was signed
| `signers` | `array` | An array of signer objects with details about each signer

#### Payload example

```json
{
  "documentId": "8bfae710-5e4b-4464-ab7a-167f73c37590",
  "externalDocumentId": "8577545740",
  "signedTime": "2017-03-01T13:00:00Z",
  "signers": [
    {
      "signerId": "954393cf-1086-4a2b-a98a-97e1feeded87",
      "signerName": "John Doe",
      "signedTime": "2017-03-01T13:00:00Z",
      "dateOfBirth": "1988-01-01",
      "signatureMethod": "no_bankid",
      "socialSecurityNumber": "01018812345"
    }
  ]
}
```

### EidSelectedEvent

#### Payload

| key        | type     | description |
| ------------- |:-------------:|:-------------:|
| `eid` | `string` | The selected eID

#### Payload example

```json
{
  "eid": "no_bankid"
}
```


### LanguageChangedEvent

#### Payload

| key        | type     | description |
| ------------- |:-------------:|:-------------:|
| `language` | `string` | The selected language code (ISO 639)

#### Payload example

```json
{
  "language": "EN"
}
```

### SignErrorEvent

#### Payload

| key        | type     | description |
| ------------- |:-------------:|:-------------:|
| `error` | `object` | Details about the error that occured

#### Payload example

```json
{
  "error": {
    "code": "cookies_disabled",
    "message": "Cookies are disabled in the users browser"
  }
}
```
