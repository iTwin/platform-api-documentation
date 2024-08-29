---

This endpoint is used to create a configuration for a PopulateFederationGuids transformation.

Populate Federation Guids transformation creates a new [`FederationGuid`](https://www.itwinjs.org/bis/guide/fundamentals/federationguids/) property value on elements that currently have `FederationGuid` value set to `null`.

This transformation is useful in [iModel Forking](https://developer.bentley.com/apis/imodels-v2/operations/fork-imodel/) scenarios when iModel fork creation in iModels API [fails with `sourceIsMissingFederationGuids` state](https://developer.bentley.com/apis/imodels-v2/operations/fork-imodel/#sourceismissingfederationguidsstate). After Populate Federation Guids transformation is run on the source iModel subsequent "Fork iModel" operations will succeed.

{!RunningTransformation.md!}

{!Authorization.md!}

{!SingleIModelPermissions.md!}

**Important**: Populate Federation Guids transformation is in closed preview mode currently and only selected applications can utilize it.

{!RateLimits.md!}

---
