---

Creates a new Changeset Group.

Changeset Groups are a way to logically group [Changesets](https://www.itwinjs.org/learning/glossary/#changeset). Changesets that belong to the same Changeset Group may be interpreted as one logical change to the iModel, for example, iModel synchronization process may create multiple Changesets but they all represent one synchronization run.

The intended workflow is as follows:

1. Application creates a Changeset Group.

2. Application pushes one or more Changesets to that Changeset Group by setting `groupId` property on the Changeset entity.

3. [Application updates Changeset Group](https://developer.bentley.com/apis/imodels-v2/operations/update-imodel-changeset-group/) and sets its `state` value to `completed`.

{!Authorization.md!}

{!iModelsPermissions.md!}

{!RateLimits.md!}

---
