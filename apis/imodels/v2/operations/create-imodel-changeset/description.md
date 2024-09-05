---

Creates the metadata of a [Changeset](https://www.itwinjs.org/learning/glossary/#changeset).

For more information on creating and retrieving Changesets using iTwin.js see [working with Changesets](https://www.itwinjs.org/learning/imodelhub/briefcases/).

 **Important: This operation should only be used by iTwin.js. For creating and uploading a valid Changeset please use iTwin.js libraries.**

Pushing a Changeset consists of three steps:

1. Create Changeset metadata.
2. Upload Changeset file to blob storage using `upload` property link from the response of Changeset metadata creation.
```
Request syntax:
    PUT upload HTTP/1.1
Request headers:
    x-ms-blob-type: BlockBlob
```

3. Complete the Changeset push by confirming that Changeset file was uploaded successfully. See [Update iModel Changeset](https://developer.bentley.com/apis/imodels-v2/operations/update-imodel-changeset/) operation for the documentation.

{!Authorization.md!}

{!iModelsPermissions.md!}

{!RateLimits.md!}

---