# OpenID Connect

Log on to our dashboard and create an OpenID Connect client and choose the OpenID connect flow that suits you usecase. If you are not sure which flow to use, we recommend read through this guide written by one of the experts in the field: [https://leastprivilege.com/2016/01/17/which-openid-connectoauth-2-o-flow-is-the-right-one/](https://leastprivilege.com/2016/01/17/which-openid-connectoauth-2-o-flow-is-the-right-one/).

## OpenID discovery endpoints

* Test: [https://oauth2test.signere.com](https://oauth2test.signere.com)
* Production [https://oauth.signere.no](https://oauth.signere.no)

## Social security number

In order to retrieve an user's social security number through OpenID you must request an access token with the "ssn"-scope, and use that access token to call the UserInfo-endpoint. We do not return the social security number as an identity token claim due to its sensitivity.

