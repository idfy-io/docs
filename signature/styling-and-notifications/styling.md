# Styling

The signature API allows you to set the color theme and main spinner for the signature app, if you want to you can even have different color themes per signer. To include theming, simply set the ui property of the signer as shown below.

## Preview


<iframe src="https://sign-test.idfy.io/theme-preview" height="750" width="100%" frameborder="0" allowfullscreen="allowfullscreen"> </iframe>


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



