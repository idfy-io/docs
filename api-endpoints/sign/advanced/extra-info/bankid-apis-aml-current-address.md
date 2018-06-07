# BankID Api's Aml Current Address

Retrieves basic address information from the official address registry

## Example request \(Create document request\)

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

## Example response \(get document\)

```text
{
    ...
    "signers": [
        ...
        "links" : [{
            "href": "https://api.idfy.io/blablabla",
            "rel": "bankIDApisAmlCurrentAddress",
            "contentType": "application/json"
        }]
        ...
    ]
    ...   
}
```

## Example data \(Retrieved from links array on signer in response\)

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

