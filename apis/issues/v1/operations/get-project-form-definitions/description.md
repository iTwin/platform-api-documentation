---

Retrieves a list of Approved form definitions for the project with the given ID.  This only returns the definition's name, type, and ID. The full definitions will be returned in the 'Get form definition by ID' endpoint.

Note that in order to create an issue, it must be associated with the ID of one of these form definitions (through the 'formId' property in the 'Create issue' request body). This API cannot be used to create or edit form definitions. They can only be created/edited/imported by project administrators through the Bentley Form Manager webapp, which is accessible at https://connect-formmanager.bentley.com/designer/#/your-itwin-id (replace `your-itwin-id` with your actual project or iTwin ID).

Note that the 'iTwinId' query string parameter is required. It must be a valid iTwin or project GUID to get form definitions from. Older clients can continue to use 'projectId' as an alias for 'iTwinId'.

{!Authorization.md!}

---