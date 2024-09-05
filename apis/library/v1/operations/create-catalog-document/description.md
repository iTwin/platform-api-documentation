---

Creates a catalog document in user's organization context.

### Notes

To create a catalog document, displayName extension and purpose are required properties.

Document purpose values are:
-Thumbnail 
-Reference

### Uploading Associated File

To complete the process, associated file should be uploaded to fileUrl (property in response) and a subsequent update document request should be made by setting 'available' property to true.

{!Authorization.md!}

{!LibraryPermissions.md!}

{!RateLimits.md!}

---