---

This endpoint is used to query a configuration entity with a provided configurationId.

**Note:** the type of `configuration` in operation response is a union of different configuration types. Configuration type is denoted by `transformType` property. API consumers should expect that new configuration types will added in the future. New configurations may have a different schema than the ones that currently exist so `configuration` should be deserialized based on `transformType`.

{!Authorization.md!}

{!iModelsPermissions.md!}

{!RateLimits.md!}

---