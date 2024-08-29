---

Retrieves the actual file contents for the attachment with the given ID. This API will attempt to infer the MIME type to return from the file's extension, but will return the default value of `application/octet-stream` if it does not recognize the extension.

### Permissions

To use this endpoint, the user is required to have the Forms **View** (`Forms_ViewAccess`) permission for the iTwin, or for the form's definition if form definition security is specified. (Having any other Forms permission automatically grants the **View** permission as well.)

{!Authorization.md!}

---