---

Creates a new issue. The user must specify the ID of a form definition to associate the issue with; that will set its issue type as well as determine how clients such as the CONNECT Issues web app will display it. The form definition ID should be obtained by calling the 'Get iTwin form definitions' endpoint.

### Permissions

To use this endpoint, the user is required to have the Forms **Create/Modify** (`Forms_CreateAccess`) permission for the iTwin, or for the chosen form definition if form definition security is specified for it.

{!Authorization.md!}

---