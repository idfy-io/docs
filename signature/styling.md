# Styling

The signature API allows you to set the color theme and main spinner for the signature app, if you want to you can even have different color themes per signer. 
To include theming simply set the ui property of the signer as shown below. 

## Preview
Visit [this page](https://sign-test.idfy.io/theme-preview) to see a preview of the different themes

<iframe width="560" height="315" src="https://sign-test.idfy.io/theme-preview" frameborder="0"></iframe>

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
