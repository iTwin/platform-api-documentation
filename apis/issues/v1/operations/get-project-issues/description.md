---

Retrieves a list of issues for the iTwin or project with the given ID. If the Prefer header is omitted, or set to "return=minimal", this only returns basic info about each issue--its ID, display name, type, subject, and whether it is in an Open, Closed, or Draft state. Setting the Prefer header to "return=representation" will return more data. Use the "Get Issue Details" endpoint to see full information about a particular issue.

Note that the 'iTwinId' query string parameter is required. It must be a valid project GUID to get issues from. Existing clients can continue to use the 'projectId' paramater as an alias for 'iTwinId'.

### Permissions

To use this endpoint, the user is required to have the Forms **View** permission (`Forms_ViewAccess`) for the iTwin, or for some issues' associated form definitions if form definition security is specified. (Having any other level of Forms permission for an issue automatically grants the **View** permission as well for that issue. If a user does not have permission to view a particular issue, it will be silently excluded from the list.)

{!Authorization.md!}

---