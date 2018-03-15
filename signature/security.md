# Security

Additional security can be added to your documents

### Auth before sign

If the documents are of the sensitive type you should include auth before sign. Auth before sign requires the user to authenticate themselves before they can open the document to be signed. To use auth before sign you either need the signer's social security number, or their id providers unique Id \(i.e. the norwegian bankid pid\).

Auth before sign has to be set on each signer in the create document request.

###### Example request

```
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



