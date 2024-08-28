---

Closes an existing Changeset Group.

Please refer to [Create iModel Changeset Group](https://developer.bentley.com/apis/imodels-v2/operations/create-imodel-changeset-group/) operation documentation for information about the purpose of Changeset Groups.

Closing a Changeset Group means that there will be no more [Changesets](https://www.itwinjs.org/learning/glossary/#changeset) in the logical group, for example, synchronization process has processed all iModel changes and will not push any more Changesets. If a Changeset Group is closed, meaning its `state` property value is `completed`, `timedOut` or `forciblyClosed`, no more Changesets referencing that particular Group will be accepted. Users can only close the Changeset Group by setting `completed` state value as other values are set by iModels API.

{!Authorization.md!}

{!iModelsPermissions.md!}

{!RateLimits.md!}

---
