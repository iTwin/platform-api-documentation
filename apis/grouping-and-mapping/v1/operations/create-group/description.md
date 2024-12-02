---

Creates a group. A group is a collection of design elements from an iModel represented by an [ECSQL](https://www.itwinjs.org/learning/ecsql/) query. When used for reporting a group represents a single output data table in a report. There are two ways to create a group.

### Create a group without properties

To create a group without properties do not provide the `source` property.

### Create a group from an existing group

To create a group from another group provide the `source` property. The server will create a new group and copy over all properties from the group referenced by the `source` property. User must have `imodels_read` permissions to the iModel containing the source group. Changing source group or its properties will not change the copies of them.

Provided `groupName`, `description`, `query`, `metadata` request body properties will overwrite the properties on the copied group.

### Note

The `query` request body property must be provided even when copying a group. Provide the source group query in the request when copying a group if you want to keep the same query.

{!GroupQuery.md!}

{!Authorization.md!}

{!GroupingAndMappingPermissions.md!}

{!RateLimits.md!}

{!ExtractionRowLimiting.md!}

---
