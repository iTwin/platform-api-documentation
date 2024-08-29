---

Retrieves a list of Approved form definitions for the iTwin with the given ID.  This only returns the definition's name, type, and ID. The full definitions will be returned in the 'Get form definition by ID' endpoint.

Note that in order to create a form data instance, it must be associated with the ID of one of these form definitions (through the 'formId' property in the 'Create form data' request body). This API cannot be used to create or edit form definitions. They can only be created/edited/imported by iTwin administrators through the Bentley Form Manager webapp, which is accessible at https://connect-formmanager.bentley.com/designer/#/your-itwin-id (replace `your-itwin-id` with your actual project or iTwin ID).

Note that the 'iTwinId' query string parameter is required. It must be a valid iTwin or project GUID to get form definitions from.  Existing clients can continue to use the 'projectId' parameter as an alias for 'iTwinId'.

{!Authorization.md!}

---