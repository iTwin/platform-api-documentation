---

Returns the information about iModel creation process.

This endpoint should be used to check if iModel creation completed.

### Forked and cloned iModels

When an iModel is a clone, the `clonedFrom` response entity property will contain information about the source iModel from which this iModel was created, otherwise it will be `null`. For more information on iModel cloning please refer to the [Clone iModel](https://developer.bentley.com/apis/imodels-v2/operations/clone-imodel/) operation documentation.

When an iModel is a fork, the `forkedFrom` response entity property will contain information about the main iModel from which this iModel was created, otherwise it will be `null`. For more information on iModel forking please refer to the [Fork iModel](https://developer.bentley.com/apis/imodels-v2/operations/fork-imodel/) operation documentation.

To get the details of the source/main iModel use [Get iModel Details](https://developer.bentley.com/apis/imodels-v2/operations/get-imodel-details/) operation with id value taken from `clonedFrom.iModelId` or `forkedFrom.iModelId`.

{!Authorization.md!}

{!iModelsPermissions.md!}

{!RateLimits.md!}

---
