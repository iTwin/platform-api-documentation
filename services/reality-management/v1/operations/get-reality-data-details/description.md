---

Retrieves the metadata of a [reality data](https://www.itwinjs.org/learning/glossary/#realitydata).

The `iTwinId` parameter is optional, but it is preferable to provide it, because the permissions used to access the collection of reality data are determined from the iTwin. With no iTwin specified, the desired reality data can be retrieved (e.g. the caller is the owner), but it's more likely to get the expected result if you provide the `iTwinId`.

{!Authorization.md!}

{!iTwinsRBACPermission.md!}

{!RateLimits.md!}

---