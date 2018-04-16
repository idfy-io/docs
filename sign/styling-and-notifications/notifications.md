# Notifications

in our signature API you can specify if you want us to notify the signers with email and/or sms for you. Our notification service let's you manage a lot of the content in the notification, if you want to of course. We also supply standard texts if you want the quick and easy solution.

Structure:  
The create document request has a notification object where you can specify core settings which will be shared between the signers. This is where you setup arrays of texts for given languages if you want to create your own. In addition to this core object you have to specify what kind of notifications each signer should get.

## Implementation

### Step 1

Decide when you want each signer to be notified by including a notifications object per signer \(this object can be null on the signers you don't want to notify\)

#### Request example

```text
  {
      ....
      "signers": [ { 
          ...
          "notifications": {
            "setup": { 
            "request": "sendBoth",
            "reminder": "sendEmail",
            "signatureReceipt": "sendSms",
            "finalReceipt": "off"
          },
          "signerInfo": {
              "mobile": {
                  "countryCode": "+47",
                  "number": "99999999"
              },
              "email": "test@test.com"
          }
          ...
      }]
      ....
  }
```

**Remarks**

Mobile must contain a valid number and country code. The country code must either start with + \(i.e. +47\) or no prefix \(i.e. 47\).

### Step 2

Setup core notification settings if you want to create your own texts, include documents as an attachment in the mail \(Beware of the security issues when sending sensitive documents by email\). If you are using reminders you also have to specify a cron expression for the reminder interval.

You can create texts in differnt languages, these will then be matched to the languages you have sat on the signers \(under ui object\). If no language is specified it will default to the english text.

#### Request example

```text
  {
      ....
      "notification": {
        "signRequest": {
          "includeOriginalFile": true,
          "email": [{
            "language": "en",
            "subject": "Signing of house contract",
            "text": "Please sign this contract .....",
            "senderName": "Test"
          }],
          "sms": [...]
          }
        }
      ....
  }
```

### Step 3

You are now ready to go! See advanced for more features

## Advanced

### Notification merge fields

If you create your own notification texts you can include some "merge-fields" in your text, when the notification is due we will replace the mergefield with the appropriate data. We currently support the following fields:

| Key | Description |
| --- | --- |
| {document-title} | We insert the title of the document |
| {document-description} | We insert the description of the document |
| {deadline} | We insert the deadline to sign the document |
| {signed-time} | \(For use in signatureReceipt, format: HH:mm:ss\) |
| {signed-date} | \(For use in signatureReceipt, format: dd.MM.yyyy\) |
| {signed-name} | \(For use in signatureReceipt, we insert the name retrieved from the signature method provider\) |
| {signature-method} | \(For use in signatureReceipt, specifies which signature method was used \) |
| {url} | We insert the sign url here. Will only work on request and reminder sms notifications \(in email notifications the sign url is always included as a button themed with the same color as the sign application\) |

You can use them in your text like this:

* The document with title {document-title} is now ready to be signed.... 
* You must sign the document titled {document-title} before {deadline}...

### Signer specific merge fields

If you setup your own email texts for the document, you may want part of the text to be specific per signer. To solve this we have introduced signer specific merge fields. They work the same way as the regular merge fields above, only you control both the key and value. Just include a dictionary of mergeFields per signer, we will then search for these keys in your text, and insert the value if it exists.

### Reminder schedule

If you setup reminders you need to specify a schedule in cron format \(quartz\). There are multiple resources on the web to help you set up the schedule. Here are some of them:

* [https://www.freeformatter.com/cron-expression-generator-quartz.html](https://www.freeformatter.com/cron-expression-generator-quartz.html)
* [http://www.quartz-scheduler.org/documentation/quartz-2.x/tutorials/crontrigger.html](http://www.quartz-scheduler.org/documentation/quartz-2.x/tutorials/crontrigger.html)

