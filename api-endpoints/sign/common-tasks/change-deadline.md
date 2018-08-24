# Change deadline

## On document

If you need the change the document deadline you can do it by doing a [document update](https://developer.idfy.io/api#operation/Documents_Update) like this:

```text
{
  "advanced": {
      "timeToLive": {
        "deadline": "2018-05-12T08:50:03Z",
      }
  }  
}
```

## On signer

If you need the change when a signer url expires you can do it by doing a [signer update](https://developer.idfy.io/api#operation/Signers_Update) like this:

```text
{
    "signUrlExpires":"2018-05-12T08:50:03Z"
}
```

