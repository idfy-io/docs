### Advanced settings

Enjoy some of the more advanced settings

### Tags

###### Document tags

Why add document tags?

* You can query your documents with tags at a later time
* The tag is included in webhooks and events, this way it is easy to separate document events based on tags

###### Example \([Create document](https://developer.idfy.io/api#operation/Documents_Create "Create document")\)

```
{
    ...

    "advanced": {
        "tags": [
          "departement_2",
          "sales"
        ]
    ...

}
```

### Departement Id

If you want to mark the documents on your invoice with separate departements you should specify it in the departementId field

###### Example \([Create document](https://developer.idfy.io/api#operation/Documents_Create "Create document")\)

```
{
    ...

    "advanced": {
        "departmentId": "A-1702"
    }
    ...

}
```

### Get social security number

If your bankid certificate allows it, you can retrieve the signers social security number

###### Example \([Create document](https://developer.idfy.io/api#operation/Documents_Create "Create document")\)

```
{
    ...

    "advanced": {
        "getSocialSecurityNumber": true
    }
    ...

}
```

### Time to live

You can specify how long a signature job should live \(default/maximum 45 days\), how long we keep the document after it is signed \(default/maximum 7 days\) and how long each signer has to sign the document \(defaults to document deadline\).

###### Example 1 \([Create document](https://developer.idfy.io/api#operation/Documents_Create "Create document")\) - Document deadline and delete after hours

```
{
    ...

    "advanced": {
        "timeToLive": {
            "deadline": "2018-02-20T07:58:05Z",
            "deleteAfterHours": 5
        }
    }
    ...

}
```

###### Example 2 \([Create document](https://developer.idfy.io/api#operation/Documents_Create "Create document")\) - Signer deadline

```
{
    ...

    "signers": [{
        ...
        "signUrlExpires": "2018-02-18T07:58:05Z"
        ...        
    }]
    ...

}
```





