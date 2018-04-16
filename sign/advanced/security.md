# Security

Security

Additional security can be added to your documents

## Auth before sign

If the documents are of the sensitive type you should include auth before sign. Auth before sign requires the user to authenticate themselves before they can open the document to be signed. To use auth before sign you either need the signer's social security number, or their id providers unique Id \(i.e. the norwegian bankid pid\).

Auth before sign has to be set on each signer.

### Example \([Create document](https://developer.idfy.io/api#operation/Documents_Create)\)

```text
{
      ....
      "signers": [ { 
          ...          
          "authentication": {
              "authBeforeSign": true,
              "socialSecurityNumber": "12345678987",
              "signatureMethodUniqueId": null
          }
          ...
      }]
      ....
  }
```

## Ip-whitelist

Coming soon

## One time use

Coming soon

## Csp

If you are implemeting a strict csp policy when iframing our solution you need to enable include the following framesources

### Eid

```text
"https://appletk.danid.dk", "https://applet.danid.dk", "blob:", "https://csfe-preprod.bankid.no",
"https://csfe.bankid.no", "https://services.bankid.no", "*.buypass.no",
"https://tupas.nordea.fi", "https://online.s-pankki.fi", "https://kultaraha.op.fi", 
"https://verkkopankki.sampopankki.fi", "https://tunnistepalvelu.samlink.fi",
"https://auth.aktia.fi", "https://online.alandsbanken.fi", "https://online.s-pankki.fi", 
"https://tupas.saastopankki.fi", "https://tupas.poppankki.fi"
```

### Signature

```text
"https://sign-api-test.idfy.io", "https://sign-api.idfy.io", "https://sign-test.idfy.io", 
"https://sign.idfy.io"
```

### Identification \(if using eaccept or auth before sign\)

```text
"https://id.signere.no","https://idtest.signere.no","https://id2.signere.no", 
"https://id.idfy.io", "https://id-test.idfy.io", "https://id2.idfy.io"
```

