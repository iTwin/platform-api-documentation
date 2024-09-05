---

Create a new iTwin. 

The user that creates the iTwin will automatically be given the `iTwin owner` role on the iTwin. This will give that user full access to the iTwin, including the ability to create new child iTwins under the iTwin they are creating. After the iTwin is created, the `iTwin owner` role can be removed from the user or granted to other users.

{!Authorization.md!}

### Authorization
The user must have the `itwins_create` permission on the parent iTwin specified in the request. If there is no parent iTwin in the request then the user must have the `itwins_create` permission on the [Account iTwin] (https://developer.bentley.com/apis/iTwins/overview/#account).

An Organization Administrator can create iTwins for their Organization.

{!iTwinAdminOnlyAuthorization.md!}

---
