---

Retrieves the container's link for an instance of [reality data](https://www.itwinjs.org/learning/glossary/#realitydata).

A container is where the reality data itself (a point cloud, a mesh, a collection of images, ...) is stored.

The container's link will allow you to upload/download data directly to this container.

A [reality data](https://www.itwinjs.org/learning/glossary/#realitydata) is always associated to exactly one container.

The `projectId` parameter is optional, but it is preferable to provide it, because the permissions used to access the container are determined from the project. With no project specified, the operation can succeed in some cases (e.g. the user is the reality data's owner), but we recommend to provide a `projectId`.

In future API versions, containers could be hosted in in different cloud providers, but for now, only Azure cloud is supported.

To store or retrieve data from a container, refer to the [Azure Blob Storage documentation](https://docs.microsoft.com/en-us/azure/storage/blobs/).

{!Authorization.md!}

### Authorization

User must be an Organization Administrator for the Organization that owns a given Project or have `RDS_USE` permission for read access and `RDS_MANAGE` permission for write access assigned at the Project level.

An Organization Administrator must have at least one of the following roles assigned in User Management: Account Administrator, Co-Administrator, or CONNECT Services Administrator. For more information about User Management please visit our Bentley Communities Licensing, Cloud, and Web Services wiki page.

{!RateLimits.md!}

---