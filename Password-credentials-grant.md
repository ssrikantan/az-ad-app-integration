# Resource owner Password credentials grant - Application authentication scenario 

An inhouse, trusted Application needs to invoke a REST API that is protected using Azure AD. This trusted application has to run under the context of a designated user/account, and no interactive User sign in should be required to access the REST API. 
This example builds on the flow that is already covered in the Open ID Connect scenario, in this repository. Refer to that for details about registering the secure API, the client Side application, etc. This article Page focussed merely on using the Postman tool to use the Password credentials grant to obtain an access token with which to call the secure API.

### 1. Using the Postman tool (calling Application) to get an auth code & access token
The request Header contains the App ID, Secret of the calling Application and the user credentials of the Account that would be used to execute the REST API call. See screenshot below.

![GitHub Logo](/images/accesstoken3.png)

### 2. Using the Postman tool to call the secure API
Use the access token returned above as a 'bearer token' to invoke the API. See below. The REST API has parsed the access/JWT Token to retrieve the user name and returned that in the response.

![GitHub Logo](/images/callsecureapi3.png)

