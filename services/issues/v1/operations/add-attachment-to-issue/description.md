---

Adds a new attachment to the specified issue. This only creates the attachment metadata; the file will need to be uploaded through a subsequent PUT call to the URL returned in the Location header of this endpoint's response.

### Permissions

To use this endpoint, the user is required to have the Forms **Comment** (`Forms_CommentAccess`) permission for the iTwin, or for the issue's associated form definition if form definition security is specified. (Having **Create/Modify**, **Assign**, **Approve**, or **Full** permission automatically grants the **Comment** permission as well.)

{!Authorization.md!}

---