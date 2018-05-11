# Change deadline

### On document

If you need the change the document deadline you can do it by doing a [document update](https://developer.idfy.io/api#operation/Documents_Update) like this:

```
{
  "advanced": {
      "timeToLive": {
        "deadline": "2018-05-12T08:50:03Z",
      }
  }  
}
```

###### Note: The deleteAfterHours property has to be set accordingly if you dont want the default value of 168 hours. \(If set to &lt;= 0 it will get the default value\)

### On signer

If you need the change when a signer url expires you can do it by doing a [signer update](https://developer.idfy.io/api#operation/Signers_Update) like this:

```
{
    "signUrlExpires":"2018-05-12T08:50:03Z"
}
```



