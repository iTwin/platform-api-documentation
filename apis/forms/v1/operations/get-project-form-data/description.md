---

Retrieves a list of form data instances for the iTwin with the given ID. If the Prefer header is omitted, or set to "return=minimal", this only returns basic info about each form--its ID, display name, type, and whether it is in an Open, Closed, or Draft state. Setting the Prefer header to "return=representation" will return more data. Use the "Get Form Data Details" endpoint to see full information about a particular form.

Note that the 'iTwinId' query string parameter is required. It must be a valid iTwin or project GUID to get forms from. Old clients can continue to use the 'projectId' parameter as an alias for 'iTwinId'.

### Permissions

To use this endpoint, the user is required to have the Forms **View** permission (`Forms_ViewAccess`) for the iTwin, or for some forms' definitions if form definition security is specified. (Having any other ProjectWise Forms permission automatically grants the **View** permission as well. If a user does not have permission to view a particular form, it will be silently excluded from the list.)

{!Authorization.md!}

---