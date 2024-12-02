---

Creates an [iModel](https://www.itwinjs.org/learning/glossary/#imodel).
There are three different ways to create an iModel.

### Create an empty iModel
 To create an empty iModel do not provide `template` and `baselineFile` properties.

### Create an iModel from an existing iModel
 To create an iModel from another iModel provide `template` property. The server will apply changesets up to the one specified by `changesetId` property to the source iModel file and use it as a Baseline File for the newly created iModel. User must have `imodels_read` permissions to the source iModel. Source and target iTwins must be in the same data center.

### Create an iModel using a Baseline File.
Creating an iModel using a Baseline File allows to upload a custom iModel file that will become the base file of the created iModel. There are three steps in creating an iModel from a Baseline File:

1. Create a new iModel and provide `baselineFile` property. **It is important to provide correct file size or the iModel creation will fail in the later steps.**

2. Upload Baseline File to blob storage using `upload` property link from the response of iModel creation.
```
Request syntax:
    PUT upload HTTP/1.1
Request headers:
    x-ms-blob-type: BlockBlob
```

3. Complete the iModel creation by confirming that Baseline File was uploaded successfully. See [Complete iModel Baseline Upload](https://developer.bentley.com/apis/imodels-v2/operations/complete-imodel-baseline-file-upload/) operation for the documentation.

### iModel initialization

When creating an empty iModel it will be initialized immediately. When creating an iModel using `template` or `baselineFile` properties initialization will be scheduled and it's state is reflected in the `state` property. For a more detailed information about initialization state see [Get iModel Baseline File](https://developer.bentley.com/apis/imodels-v2/operations/get-imodel-baseline-file-details/) operation.

{!Authorization.md!}

{!iModelsiTwinPermissions.md!}

### Rate limits

This operation has a lower rate limit than the rest of iModels API operations. If an application exceeds the rate limit it will receive an HTTP error code 429 "Too Many Requests". The error response includes a Retry-After header that indicates how long clients should wait before retrying.

| Tier                       | Rate limit          |
| -------------------------- | ------------------- |
| Trial                      | 5 calls per minute  |
| Basic, Premium, Enterprise | 50 calls per minute |
<br/>
---