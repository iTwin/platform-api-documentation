---

Update file

{!Authorization.md!}

{!RbacPermissions.md!}

### Errors

This request can return InvalidCreateFileRequest error with 422 status code. This could happen because of these reasons:

- File name contains invalid characters.
- File name's length is larger than 255 characters.
- File could be harmful. For example, executable files are not accepted.

---
