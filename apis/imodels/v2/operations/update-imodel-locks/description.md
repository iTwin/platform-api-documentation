---

Acquires requested locks on specified objects.
Lock - the right to modify a specific type of data within the iModel. For more information on Locks [see working with Locks via iTwin.js client libraries](https://www.itwinjs.org/learning/backend/concurrencycontrol/#pessimistic-concurrency-control).

**Note:** Lock types have been removed for this API and should be ignored.

**Object ids Limit:** Currently there can be at most 1000 object ids in a single request.

{!Authorization.md!}

### Authorization

To release any Locks (set `LockLevel` to `none`) user must have `imodels_manage` permission assigned at the iModel level. If permissions at the iModel level are not configured, then user must have `imodels_manage` permission assigned at the iTwin level. To acquire or realese Locks that the user owns `imodels_write` permission is enough.

Alternatively the user should be an Organization Administrator for the Organization that owns a given iTwin the iModel belongs to.

For more information please refer to [Account Administrator](https://developer.bentley.com/apis/access-control-v2/overview/#accountadministrator) documentation section on Access Control API documentation page.

{!RateLimits.md!}

---
