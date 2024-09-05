---

Retrieves details of a validation run for the run specified by the run id.

- Links are included to retrieve the associated test and result. The run status in the response can be polled periodically as the agent job completes asynchronously. Calling the link to get the result before the run status is 'completed' will return a 202 response.

- Discover run ids by calling [GET /validation/propertyValue/runs](/api-groups/validation/apis/validation/operations/get-validation-propertyvalue-runs/)

{!Authorization.md!}

---
