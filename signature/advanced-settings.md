# Advanced settings

Enjoy some of the more advanced settings

### Tags

###### Document tags

Why add document tags?

* You can query your documents with tags at a later time
* The tag is included in webhooks and events, this way it is easy to separate document events based on tags

###### Example \(Create document\)

```
{
    ...

    "Advanced": {
    "Tags": [
      "departement_2",
      "sales"
    ]

    ...

}
```

### Departement Id

If you want to mark the documents on your invoice with separate departements you should specify it in the departementId field

###### Example \(Create document\)

```
{
    ...

    "Advanced": {
    "departmentId": "A-1702"
    }
    ...

}
```



