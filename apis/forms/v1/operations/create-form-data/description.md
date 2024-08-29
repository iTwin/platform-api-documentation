---

Creates a new form data instance. The user must specify the ID of a form definition to associate the instance with; that will set the instance's form type as well as determine how clients such as the CONNECT Forms web app will display it. The form definition ID should be obtained by calling the 'Get iTwin form definitions' endpoint.

### Permissions

To use this endpoint, the user is required to have the Forms **Create** (`Forms_CreateAccess`) permission for the project, or for the form's definition if form definition security is specified.

{!Authorization.md!}

---