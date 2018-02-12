# Styling

Idfy signing services are highly customizable. Below is a list of some of the things that can be customized in our signing services:

* Logo in the signing page
* Theme colors in the signing UI
* Spinner type when loading documents for signing
* Notification text \(both sms and email\)
* Email text and email colors.

The signature API allows you to set the color theme and main spinner for the signature app, if you want to you can even have different color themes per signer. To include theming, simply set the ui property of the signer as shown below.

## Preview

&lt;div class="iframe\_container"&gt;

&lt;iframe src="[https://sign-test.idfy.io/theme-preview](https://sign-test.idfy.io/theme-preview)" height="500" width="600" frameborder="0" allowfullscreen="allowfullscreen"&gt; &lt;/iframe&gt;

&lt;/div&gt;

## Request example

```
{
...
"signers": [{
      "ui": {        
        "styling": {
          "colorTheme": "Teal",
          "spinner": "Document"
        }
      }
    }
  ],  
  ...
}
```



