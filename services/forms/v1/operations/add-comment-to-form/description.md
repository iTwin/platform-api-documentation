---

Adds a new comment to the specified form data instance. Only the comment text is needed; the author and creation time will be automatically set by the server.

### Permissions

To use this endpoint, the user is required to have the Forms **Comment** (`Forms_CommentAccess`) permission for the iTwin, or for the form's definition if form definition security is specified. (Having **Create/Modify**, **Assign**, **Approve**, or **Full** permission automatically grants the **Comment** permission as well.)

{!Authorization.md!}

---