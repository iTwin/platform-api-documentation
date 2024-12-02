---

Creates an iModel fork. An iModel fork is a new iModel which is a full or partial clone of the main (source) iModel, but the difference between an iModel fork and an iModel clone is that forks can be edited and then merged back to the main iModel using [Merge iModel transformation](https://developer.bentley.com/apis/transformations/operations/mergeimodel/).

### Relationship between main and fork iModels

An iModel fork is a valid standalone iModel. An iModel fork is not deleted if the main iModel is deleted.

When the iModel forking process is completed, no new changes are synchronized to the iModel fork from the main iModel.

[iModel Create Operation Details](https://dev-developer.bentley.com/apis/imodels-v2/operations/get-create-imodel-operation-details/) operation can be used to determine if the current iModel is a fork.

### iModel fork content and metadata

The iModel fork name and description can be specified when forking an iModel, by default name and description are taken from the main iModel. iModel extent is always taken from the main iModel.

[iModel Baseline](https://developer.bentley.com/apis/imodels-v2/operations/get-imodel-baseline-file-details/) is always copied from the main iModel to the iModel fork. User can specify until which point [Changesets](https://developer.bentley.com/apis/imodels-v2/operations/get-imodel-changesets/) should be copied to the iModel fork, by default all main iModel Changesets are copied. The rest of main iModel entities are not copied.

### Operation state

Forking an iModel is an asynchronous operation. To check the status of the operation please follow the link present in `Create-iModel-Operation` response header. The link points to [Get Create iModel Operation details](https://developer.bentley.com/apis/imodels-v2/operations/get-create-imodel-operation-details/) endpoint of the iModel fork. When the iModel fork's Create Operation `state` property is set to `successful` it means the forking process is complete and iModel is ready to be used.

#### `mainIModelIsMissingFederationGuids` state

If `state` returned by [Get Create iModel Operation details](https://developer.bentley.com/apis/imodels-v2/operations/get-create-imodel-operation-details/) is equal to `mainIModelIsMissingFederationGuids`, it means that iModel fork creation failed because some elements in the main iModel do not have [FederationGuid](https://www.itwinjs.org/bis/guide/fundamentals/federationguids/) property set. In order to proceed users must populate missing FederationGuid values in main iModel using [Populate Federation Guids transformation](https://developer.bentley.com/apis/transformations/operations/populatefederationguids/) and retry the iModel fork creation request.

{!Authorization.md!}

### Authorization

User must have the following permissions:
- `imodels_manage` permission at the main iModel iTwin level.
- `imodels_manage` permission at the iTwin, in which the iModel fork will be created, level.

If main iModel has iModel level permissions configured, then user must have at least `imodels_webview` permission assigned.

Alternatively the user should be an Organization Administrator both for the Organization that owns main iModel iTwin and the Organization that owns the iModel fork iTwin.

For more information please refer to [Account Administrator](https://developer.bentley.com/apis/access-control-v2/overview/#accountadministrator) documentation section on Access Control API documentation page.

**Important**: Fork iModel operation is in closed preview mode currently and only selected applications can utilize it.

### Rate limits

This operation has a lower rate limit than the rest of iModels API operations. If an application exceeds the rate limit it will receive an HTTP error code 429 "Too Many Requests". The error response includes a Retry-After header that indicates how long clients should wait before retrying.

| Tier                       | Rate limit          |
| -------------------------- | ------------------- |
| Trial                      | 5 calls per minute  |
| Basic, Premium, Enterprise | 20 calls per minute |
<br/>
---
