---

Retrieves the workflow for the given issue type in the given iTwin or project. The iTwin must be specified using the 'iTwinId' query string parameter. Existing clients can continue to use the 'projectId' parameter as an alias for 'iTwinId'.

It is possible for users of an iTwin to choose not to set a workflow for a given type. In that case, requests to get the workflow of that type will return a 404 Not Found response where the 'code' property of the body's 'error' object is set to "WorkflowNotFound". This does not indicate client or server error. Other HTTP status codes, or other values of the 'code' property, do indicate an unexpected error of some sort.

Note that workflows cannot be customized through this API; they can only be added, deleted, or changed manually by project administrators through the Bentley Form Manager webapp, found at https://connect-formmanager.bentley.com/designer/#/your-itwin-id (replace `your-itwin-id` with your actual project or iTwin ID).

{!Authorization.md!}

---