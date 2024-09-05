---

Runs Clash Detection test for the specified test ids (currently restricted to 1 test run per request) and returns the result/clash-report ids. The maximum number of clashes may be specified with the resultsLimit parameter in the request body. If none is specified, the default is 100,000.

- This API has a rate limit of 6 API calls per second.  If an application exceeds the rate limit it will receive an HTTP error code 429 "Too Many Requests". The error response includes a Retry-After header that indicates how long clients should wait before retrying.

- To retrieve the run status as the agent job completes asynchronously, use the result id to call [GET /clashdetection/results](/api-groups/validation/apis/clash-detection/operations/get-clashdetection-result/)

- Discover test ids by calling [GET /clashdetection/tests](/api-groups/validation/apis/clash-detection/operations/get-clashdetection-tests/)

- Discover iModel ids by calling [GET /imodels](/api-groups/data-management/apis/imodels-v2/operations/get-project-imodels/)

- Discover changeset ids by calling [GET /imodels/{id}/namedversions](/api-groups/data-management/apis/imodels-v2/operations/get-imodel-changesets/)

{!Authorization.md!}

---