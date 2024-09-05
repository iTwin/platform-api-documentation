---

Queries locks of the iModel.
Lock - the right to modify a specific type of data within the iModel. For more information on Locks [see working with Locks via iTwin.js client libraries](https://www.itwinjs.org/learning/backend/concurrencycontrol/#pessimistic-concurrency-control).

**Note:** Lock types have been removed for this API and should be ignored.

### Paging

Page size refers to total size of returned `objectIds` throughout all returned instances. If several Lock instances are returned that does not necessarily mean that instance is complete and more `objectIds` might be returned for that specific instance in a different page.

{!Authorization.md!}

{!iModelsPermissions.md!}

{!RateLimits.md!}

---
