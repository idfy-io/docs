# Signature



## Packaging

Bla bla sometinhg about the pades format

### Customizing and styling

Idfy signing service is very customizable bellow are a list of things that can be customized.

* Logo on the page
* Theme colors
* Spinner type
* Notification text \(both sms and email\)
* Email text and email colors.

#### Notification merge fields
If you create your own notification texts you can include some "merge-fields" in your text, when the notification is due we will replace the mergefield with the appropriate data. We currently support the following fields:

 * {document-title}
 * {document-description}
 * {deadline}
 * {signed-time} (For use in receipt, format: HH:mm:ss)
 * {signed-date} (For use in receipt, format: dd.MM.yyyy)
 * {signature-method} (For use in receipt)

You can use them in your text like this: 

- The document with title {document-title} is now ready to be signed.... 
- You must sign the document titled {document-title} before {deadline}...
