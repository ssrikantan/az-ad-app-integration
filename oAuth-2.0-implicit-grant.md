# oAuth-2.0 implicit grant - Application authentication scenario 

This applies to a scenario where A Javascript/Single Page Application (SPA) needs to invoke a REST API that is protected using Azure AD. 

In the oAuth authorization code grant scenario covered in another article page in this repo, the Client Web Application calls the Azure AD Authorization end point to sign in the user, get an access code and redirects directly to the Azure AD Token end point to get the access token. The Client Web Application then  uses this access token to call the REST API.

In the case of Implicit grant scenario that is applicable to an SPA, such a two step process with redirection is not possible, since it has to be executed from the browser directly with the Azure AD end point. Instead, the SPA Application calls only the Azure AD authorization endpoint, signs in the user and gets the access token directly (without the intermediate step involving getting the access code)

## 1. Registering the REST API with Azure AD and securing it
The steps to be performed are the same as with the Open ID Connect flow already covered.

## 2. Registering the Client Web Application with Azure AD
The steps here are also similar to that with the Open ID Connect scenario. There are some additional configurations to be done.
- Enable oAuth2 Implicit Flow (this was not required in the Open ID Connect scneario) in the Application manifest of the CLient side Application registration step. See below

![GitHub Logo](/images/webclientappregn.png)

The redirect URL in the Application Registration is set to the Postman Client call back URL. See below

![GitHub Logo](/images/redirecturl.png)

## 3. Using the Postman tool to obtain an access token from the Azure AD authorization end point
In the Postman tool, select the 'authorization option' to oAuth 2.0 and click on the 'Get new Access Token' button. In the dialog that comes up, select the 'Implicit' grant option. Note that, unlike with the Open ID Connect scenario that had both the AZure AD authorization end point and the token endpoint, here , only the Azure AD Authorization end point requires to be specified. 

**Ensure that the 'Client Authentication' option on this dialog is set to 'Send as Basic Auth Header'**

(Note that the auth endpoint URL contains the App ID of the secure Web API)
See below:

![GitHub Logo](/images/implicitgrant.png)

Clicking on 'Request Token' button takes the user to the Sign in page. On completion, the access Token is received. Unlike with the Open ID Connect Flow, there are no ID Tokens or Refresh Tokens returned.

See below
![GitHub Logo](/images/accesstoken4.png)

## 4. Use the access token returned above as a 'bearer token' to invoke the API
See below. The REST API has parsed the access/JWT Token to retrieve the user name and returned that in the response

![GitHub Logo](/images/callsecureapi2.png)
