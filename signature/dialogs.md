# Dialogs

In our signature api you can include dialogs with information to the signer. You can setup dialogs that will be displayed before and/or after the document is signed. In the dialog before you can also include a checkbox stating that the signer has understood the text before they can continue.



The dialogs object is placed under signers.ui.dialogs

#### Example request:

```
{
    ...
    signers: [
        {
            ...
            "ui": {
                "dialogs": {
                  "before": {
                    "useCheckBox": true,
                    "title": "Good luck",
                    "message": "Please read the contract on the next pages carefully. Pay some extra attention to paragraph 5."
                  },
                  "after": {
                    "title": "Thank you for your signature",
                    "message": "We will contact you when we have processed the signed contract."
                  }
            ...
        } 
    ],
    ...
}
```



### How it looks in the application

![](/assets/Dialog-Before.PNG)![](/assets/dialog-after.PNG)

