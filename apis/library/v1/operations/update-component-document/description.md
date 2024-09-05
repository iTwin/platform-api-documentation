---

Updates a component document in user's organization context.

### Notes

To update a document request body must contain all the properties desired for the document since this will replace existing document with current document definition. DisplayName extension and purpose are required properties.

Document purpose values are:
-Design
-Thumbnail 
-Reference
-GalleryImage
-TypeCatalog

### Associated Documents
Document with purpose Thumbnail, GalleryImage and TypeCatalog can have associated design document, this should be a valid Id of existing design document. PreviousVersionId is only valid for Design documents and requires a valid Id of an existing design document, in case a design document needs up-version. In case there are multiple versions of the design document, only one design document and it's corresponding thumbnail can be active.

{!Authorization.md!}

{!LibraryPermissions.md!}

{!RateLimits.md!}

---