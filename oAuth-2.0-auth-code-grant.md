## Using Auth Code grant - Application authentication

A Web Application needs to invoke a REST API that is protected using Azure AD. The calling Application authenticates a user, but does not convey the User context in the request to the REST API. It calls the REST API using the Application level access token. This flow is similar to the one with Open ID Connect which is already covered in this repository, the only difference being that instead of an Id token, and Auth token is used
