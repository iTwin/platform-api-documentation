---

Uploads a file's contents, associating it with the attachment metadata instance with the given ID. The request body is simply the file's bytes. If a file was already uploaded for the attachment with the given ID, that file will be overwritten.

### Permissions

To use this endpoint, the user is required to have the Forms **Comment** permission (`Forms_CommentAccess`) for the iTwin, or for the form's definition if form definition security is specified. (Having **Create/Modify**, **Assign**, **Approve**, or **Full** permission automatically grants the **Comment** permission as well.)

{!Authorization.md!}

---