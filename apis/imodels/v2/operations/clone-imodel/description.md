---

Clones the specified iModel. 

Cloning an iModel means that a new iModel is created by importing data from the source iModel. That new iModel is considered to be an iModel clone. Id of the source iModel is specified in the request url while the id of the target iTwin which will contain the new iModel is specified in the request body.

### Relationship between the source iModel and the iModel clone

iModel clone is a valid standalone iModel. After the iModel cloning process is completed, no new changes are synchronized to the iModel clone from the source iModel. iModel clone is not deleted if the source iModel is deleted.

### iModel clone content and metadata

The target iModel name and description can be specified when cloning an iModel, by default name and description are taken from the source iModel. iModel extent is always taken from the source iModel.

[iModel Baseline](https://developer.bentley.com/apis/imodels-v2/operations/get-imodel-baseline-file-details/) is always copied from the source iModel to the target iModel. User can specify until which point [Changesets](https://developer.bentley.com/apis/imodels-v2/operations/get-imodel-changesets/) should be copied to the target iModel, by default all source iModel Changesets are copied. The rest of source iModel entities are not copied.

### Operation state

Clone iModel is an asynchronous operation. To check the status of the operation please follow the link present in `Create-iModel-Operation` response header. The link points to [Get Create iModel Operation details](https://developer.bentley.com/apis/imodels-v2/operations/get-create-imodel-operation-details/) endpoint of the target iModel. When the target iModel's Create Operation `state` property is set to `successful` it means the cloning process is complete and iModel is ready to be used.

`Location` header value is a link to [Get iModel details](https://developer.bentley.com/apis/imodels-v2/operations/get-imodel-details/) endpoint of the target iModel which provides metadata about the the target iModel as well as when it is ready to be used. When target iModel's `state` property is set to `initialized` the iModel is ready to be used.

Please note that iModel may be marked as `initialized` before the iModel Create Operation is marked as `successful`. Such behavior allows target iModel to be utilized faster. The cloning background process first of all copies the critical iModel data and marks the iModel as `initialized`, and then copies additional data used to improve performance for iModel viewing and authoring workflows.

{!Authorization.md!}

### Authorization

User must have the following permissions:
- `imodels_manage` permission at the source iModel iTwin level. 
- `imodels_manage` permission at the target iTwin level. 

If source iModel has iModel level permissions configured, then user must have at least `imodels_webview` permission assigned at iModel level.

Alternatively the user should be an Organization Administrator both for the Organization that owns source iModel iTwin and the Organization that owns target iTwin.

For more information please refer to [Account Administrator](https://developer.bentley.com/apis/access-control-v2/overview/#accountadministrator) documentation section on Access Control API documentation page.

### Rate limits

This operation has a lower rate limit than the rest of iModels API operations. If an application exceeds the rate limit it will receive an HTTP error code 429 "Too Many Requests". The error response includes a Retry-After header that indicates how long clients should wait before retrying.

| Tier                       | Rate limit          |
| -------------------------- | ------------------- |
| Trial                      | 5 calls per minute  |
| Basic, Premium, Enterprise | 20 calls per minute |
<br/>
---
