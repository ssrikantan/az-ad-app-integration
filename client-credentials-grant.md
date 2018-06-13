# Application authentication scenario 

A daemon or Server Application needs to invoke a REST API that is protected using Azure AD. There is no user interaction possible for the daemon application which has to have an Application Identity to gain access to the API. oAuth 2.0 Client credentials grant, as described here - https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-authentication-scenarios is used in this scenario. 
