---

Updates the metadata of a [reality data](https://www.itwinjs.org/learning/glossary/#realitydata).

The `projectId` parameter is optional, but it is preferable to provide it, because the permissions used to allow the modification of the reality data are determined from the project.

With no project specified, it may be possible to modify the reality data (e.g. the caller is the owner), but more permissions may be granted when the `projectId` is provided.

{!Authorization.md!}

{!RbacPermissions.md!}

{!RateLimits.md!}

---