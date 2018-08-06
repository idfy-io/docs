# Extra info

## Get started

Our signature API allows you to seamlessly integrate extra information into the response, please see the available types below.

## Available types

### Signer

> personalInfo
>
> companyInfo
>
> companyInfoAutoComplete
>
> personalCreditCheck
>
> businessCreditCheck
>
> officialPersonalInfo
>
> [bankIDApisAmlPersonSanctionPep](bankid-apis-aml-person-sanction-pep.md)
>
> [bankIDApisAmlCurrentAddress](bankid-apis-aml-current-address.md)

### Document

> rightsAndProkura



## When is the information ready?

If you need the information immediately after the signer has completed the signature, and are running our application in an iframe. The easiest way to collect the info is to let the signer wait a few seconds while the requested information is processed. 

To do that you need to log into the [idfy dashboard](https://dashboard.idfy.io/login) and complete the following steps:

1. Find your account: Account -&gt; view account 
2. Find "Settings API" on the account menu
3. Find signature settings and click override
4. Choose the desired success action
   * Continue when resources complete if you dont need to wait on the file packaging right now \(faster\)
   * Continue when all is complete if you need both the signed files and the resources to be ready before the signer is proceeding to your success page
5. Optional: Set max polltime in seconds \(defaults to 30\), if the files is not ready within this time the signer is sent to the error page. It may not be an exact match because the polling schedule goes like this: poll -&gt; wait 1 sec -&gt; poll -&gt; wait 2 sec -&gt; poll wait 3 sec -&gt; and so on. If a poll is initiated it will run this before going to error.



An alternative approach is to listen for the [resource created event](https://docs.idfy.io/api-endpoints/notification/events#resourcecreatedevent) as a webhook or in the .Net events client.

## Error handling

If you are using the webmessage/iframe approach you should handle errors accordingly. The relevant [error codes is](https://docs.idfy.io/api-endpoints/sign/other-information/error-codes):

SA-1030: The resources/files was not ready within the specified max poll time

SA-1031: A generic error occured when checking the signature status

SA-1032: The extra information / resource could not be fetched because of an error specific to this resource









