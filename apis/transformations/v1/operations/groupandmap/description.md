---

This endpoint is used to create the Group And Map configuration.

The Group And Map transformation enables the creation of new custom EC schemas and is capable of remapping already existing elements to the new EC classes with new EC properties. The custom schema is constructed using grouping and mapping data. It is your responsibility to create a valid mapping for the source iModel through [the Reporting API](/apis/insights/) before starting the transformation. To learn more about EC schemas and classes, please see [Base Infrastructure Schemas](https://www.itwinjs.org/bis/).

These are the logical relations from [grouping and mapping](/apis/insights/operations/create-mapping/) data to EC schema:
```
Mapping -> EC schema
Group -> EC class
GroupProperty -> EC property
```

After the transformation all elements that were *selected* with the group query will be remapped to the corresponding EC class. These elements will also have all the new EC properties inserted. The newly inserted EC properties' values will be populated with the help of 'ecProperties' field taken from the respective GroupProperty which you configured beforehand.

POST configuration specific properties explained:
```
mappingId - source iModel mapping id.
groupOverrides - list of overrides for each group.
    - groupId - id of mapping group.
    - baseClass - base EC class that will be applied for elements selected by group.
        - ecSchemaName - EC schema name.
        - ecClassName - EC class name.
additionalEcSchemas - list of additional EC schemas that will be added to target iModel.
    - ecSchemaName - EC schema name.
    - ecSchemaVersion - EC schema version.
```
<br/>

{!TransformerMetadata.md!}

{!RunningTransformation.md!}

{!Authorization.md!}

{!iModelsPermissions.md!}

{!RateLimits.md!}

---
