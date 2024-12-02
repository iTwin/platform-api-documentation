---

Runs a property value validation test for the specified test id and returns the run id. The maximum number of validation failures may be specified with the resultsLimit parameter in the request body. If none is specified, the default is 100,000.

- This API has a rate limit of 6 API calls per second.  If an application exceeds the rate limit it will receive an HTTP error code 429 "Too Many Requests". The error response includes a Retry-After header that indicates how long clients should wait before retrying.

- A link is included to retrieve the run status as the agent job completes asynchronously.

- Discover test ids by calling [GET /validation/propertyValue/tests](/api-groups/validation/apis/validation/operations/get-validation-propertyvalue-tests/)

- Discover iModel ids by calling [GET /imodels](/api-groups/data-management/apis/imodels/operations/get-project-imodels/)

- Discover named version ids by calling [GET /imodels/{id}/namedversions](/api-groups/data-management/apis/imodels/operations/get-imodel-named-versions/)

{!Authorization.md!}

---