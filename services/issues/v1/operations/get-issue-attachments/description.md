---

Retrieves the metadata for all files attached to the given issue. In order to get the contents of a file itself, use the `Get attachment file by ID` endpoint, passing the `id` from the metadata object returned by this request as the `attachmentId` parameter of that request.

### Permissions

To use this endpoint, the user is required to have the Forms **View** (`Forms_ViewAccess`) permission for the iTwin, or for the issue's associated form definition if form definition security is specified. (Having any other level of Forms permission automatically grants the **View** permission as well.)

{!Authorization.md!}

---