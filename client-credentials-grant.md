## Using Client credentials grant - Application authentication

A daemon or Server Application needs to invoke a REST API that is protected using Azure AD. There is no user interaction possible for the daemon application which has to have an Application Identity to gain access to the API. oAuth 2.0 Client credentials grant, as described here - https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-authentication-scenarios is used in this scenario. Refer to https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-integrating-applications to understand how to register Applications in Azure AD.

### 1. Creating the REST API that is protected using Azure AD
An ASP.NET 2.0 Core Web API Project is created using Visual Studio 2017. This Project Template provides a turnkey integration with Azure AD. 
![GitHub Logo](/images/appconfig.png)

This Project Template also registers this Web API Project with Azure AD and populates the appsettings.json as shown below.

![GitHub Logo](/images/appregistration.png)

### 2. Editing the Application Manifest to add Application Roles
The manifest is edited (see above)to add Application Roles that could be used by calling Applications to gain access to the API. No user context would be passed in this scenario from the calling Application.

### 3. Registering the daemon or the calling Application with Azure AD
Create a Registration for the calling Application in Azure AD. This Application could be external to and running outside of Azure.
Configure the Client Web App to have access to the Web API registered earlier. (Note that the 'delegated permission' is not checked. Only the Application permission is selected (refer to the changes made to the manifest file of the Web API in the previous step). Click on 'Grant access' after setting the permissions. See below

![GitHub Logo](/images/clientappregn.png)

Generate a Key for the App that would be embedded in the calling Application (Postman Tool in this case), from the Settings>API Access>keys section in the Azure Portal for the Client App registered.

Obtain the oAuth Token endpoint URL that would be shared with the Calling Application to obtain the access tokens from. See below

![GitHub Logo](/images/tokenendpoint.png)

The following info needs to be shared with the calling Application to make the secure API call using Client credentials grant:
- App ID of the secure API (Step 1 above)
- App Id and secret(Key) that was generated for the calling Application, when creating a registration for it in Azure AD (step 3 above)
- The oAuth Token endpoint that would be used by the calling Application to obtain the token from.

### 4. Using the Postman tool (calling Application) to get an access token to call the secure API
Use the above information to invoke the oAuth endpoint and specify the Grant type as 'client_credentials'. This returns an access token in the response. See below

![GitHub Logo](/images/accesstoken1.png)

### 5. Using the Postman tool to call the secure API
Use the access token returned above as a 'bearer token' to invoke the API. See below

![GitHub Logo](/images/callsecureapi1.png)
