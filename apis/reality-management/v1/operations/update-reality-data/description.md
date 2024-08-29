---

Updates the metadata of a [reality data](https://www.itwinjs.org/learning/glossary/#realitydata).

The `iTwinId` parameter is optional, but it is preferable to provide it, because the permissions used to allow the modification of the reality data are determined from the iTwin.

With no iTwin specified, it may be possible to modify the reality data (e.g. the caller is the owner), but more permissions may be granted when the `iTwinId` is provided.

{!Authorization.md!}

{!iTwinsRBACPermission.md!}

{!RateLimits.md!}

---