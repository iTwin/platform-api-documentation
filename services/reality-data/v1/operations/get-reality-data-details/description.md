---

Retrieves the metadata of a [reality data](https://www.itwinjs.org/learning/glossary/#realitydata).

The `projectId` parameter is optional, but it is preferable to provide it, because the permissions used to access the collection of reality data are determined from the project. With no project specified, the desired reality data can be retrieved (e.g. the caller is the owner), but it's more likely to get the expected result if you provide the `projectId`.

{!Authorization.md!}

{!RbacPermissions.md!}

{!RateLimits.md!}

---