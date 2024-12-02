---

Extend the expiration date of a Share.

iModels Share API provides a way to publicly share an iModel. Each Share instance has a `shareKey` property which allows anonymous access to the shared iModel using iModels API.
To use the `shareKey` to access the iModel one has to provide `shareKey` via `Authorization` header: `Authorization: Basic {shareKey}`, when calling iModels API.

All Share operations interact only with the Share instances that the calling user has created. E.g. querying iModel Shares will not return all the Shares iModel has, but only the Shares which were created by the user who is calling the API.

{!Authorization.md!}

{!iModelsPermissions.md!}

**Important**: Share operations are in closed preview mode currently. Hence only selected applications can utilize the Share API.

{!RateLimits.md!}

---