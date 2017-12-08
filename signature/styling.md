# Styling

The signature API allows you to set the color theme and main spinner for the signature app, if you want to you can even have different color themes per signer. 
To include theming simply set the ui property of the signer as shown below. 

## Preview
Visit [this page](https://sign-dev.idfy.io/theme-preview) to see a preview of the different themes

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
