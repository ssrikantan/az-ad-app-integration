# Open Id Connect - Application authentication scenario 

An Application needs to invoke a REST API that is protected using Azure AD, using Open ID Connect. In this sample, the user context is passed to the secure API, which parses the JWT Token to retrieve the user name and returns that in the API response to the calling application.
(About Open ID Connect - here - https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-authentication-scenarios and https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-protocols-openid-connect-code is used in this scenario) 
Refer to https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-integrating-applications to understand how to register Applications in Azure AD.

### 1. Creating the REST API that is protected using Azure AD
An ASP.NET 2.0 Core Web API Project is created using Visual Studio 2017. This Project Template provides a turnkey integration with Azure AD. 
![GitHub Logo](/images/openidconnect_appregn.png)

This Project Template also registers this Web API Project with Azure AD and populates the appsettings.json as shown below.

### 2. Editing the Application Manifest to add Application Roles
Edit the manifest of the Application registration above, to allow oAuth 2.0 implicit flow. This is 'false' by default. See below

![GitHub Logo](/images/appregistration2.png)

### 3. Registering the calling Application with Azure AD
Create a Registration for the calling Application in Azure AD. This Application could be external to and running outside of Azure.
Configure the Client Web App to have access to the Web API registered earlier. Enable the 'delegated permission' option. Click on 'Grant Access' after setting the permissions to access the API. See below

![GitHub Logo](/images/clientappregn2.png)

Generate a Key for the App that would be embedded in the calling Application (Postman Tool in this case), from the Settings>API Access>keys section in the Azure Portal for the Client App registered.

Obtain the oAuth Token endpoint URL that would be shared with the Calling Application to obtain the access tokens from. See below

![GitHub Logo](/images/tokenendpoint2.png)

The following info needs to be shared with the calling Application to make the secure API call using Client credentials grant:
- App ID of the secure API (Step 1 above)
- App Id and secret(Key) that was generated for the calling Application, when creating a registration for it in Azure AD (step 3 above)
- The oAuth Token endpoint to get the auth code after user sign in, and use the auth code to get an access token from the oAuth authorize endpoint that would be used by the calling Application to call the API.

### 4. Using the Postman tool (calling Application) to get an auth code & access token
Use the Postman tool's ability to 'Request Token'. See below. The authorize token URL contains the App ID of the secure REST API, and an 'auth code' returned for this App ID after prompting the user to sign in. After successful sign in, the Postman tool sends a request to the auth token end point, passing the 'auth code' retrieved in the previous step, to obtain an 'auth token'. Click on 'Use token' to embed that in the request to the REST API

![GitHub Logo](/images/accesstoken2.png)

### 5. Using the Postman tool to call the secure API
Use the access token returned above as a 'bearer token' to invoke the API. See below. The REST API has accepted the auth token in the request, parsed the JWT Token to retrieve the user name and returns that in the response

![GitHub Logo](/images/callsecureapi2.png)
