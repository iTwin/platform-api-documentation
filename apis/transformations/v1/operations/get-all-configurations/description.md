---

This endpoint is used to query a list of configuration entities.

To get full configuration entities in a list set prefer header to `return=representation`.

**Note:** when `return=representation` is used, the type on entities returned in `configurations` array is a union of different configuration types. Configuration type is denoted by `transformType` property. API consumers should expect that new configuration types will added in the future. New configurations may have a different schema than the ones that currently exist so array items should be deserialized based on `transformType`.

{!Authorization.md!}

{!RateLimits.md!}

---