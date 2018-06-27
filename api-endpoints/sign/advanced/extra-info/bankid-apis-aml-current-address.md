# BankID Api's Aml Current Address

Retrieves basic address information from the official address registry. Requires the signer's [social security number](../advanced-settings.md#get-social-security-number) to be retrieved.

## Example request \([Create document](https://developer.idfy.io/api#operation/Documents_Create)\)

```text
{
    ....
    "advanced": {
        ...
            "extraInfo": {
                "types": ["bankIDApisAmlCurrentAddress"]                
            }

        ...        
    }
    ....
}
```

## Example response \([Retrieve document](https://developer.idfy.io/api#operation/Documents_Get)\)

```text
{
    ...
    "signers": [
        ...
        "links" : [{
            "href": "https://api.idfy.io/resources/59219384eb3d4552889c554ab63c8468",
            "rel": "bankIDApisAmlCurrentAddress",
            "contentType": "application/json"
        }]
        ...
    ]
    ...   
}
```

If the response only contains the `rel` property, it means that the resource is not yet available for download. The resource is usually ready within a few seconds after the signer has successfully signed the document.

If the information could not be retrieved for any reason, the response will contain an `errorMessage` describing the error. 

## Example resource response

```text
{
  "CurrentAddress": {
    "Address": "Karl Johans gate 1B",
    "Postalcode": "0154",
    "City": "Oslo",
    "Country": "NO",
    "PersonStatus": "RESIDENT",
    "AddressStatus": "ORDINARY_RESIDENT",
    "RegisteredDate": "2015-06-06T14:34:58.3179726+02:00"
  }
}
```

## Full response model

[https://aml.bankidapis.no/\#operation/AddressFromSDO](https://aml.bankidapis.no/#operation/AddressFromSDO)

