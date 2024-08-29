---

This endpoint is used to create a configuration for filtering iModel data based on an ECSql query.

ECSQL is a text-based command language for CRUD (create, read, update, delete) operations against the business data in an iModel or ECDb file. For more information, samples and tutorials see [ECSQL](https://www.itwinjs.org/learning/ecsql/).

Configuration specific properties explained:

```
ecSql - ECSql query that only selects ECInstanceIds of elements that the iModel will be filtered by.
inclusive - 'false' when all elements selected by ecSql query are filtered out, 'true' when all physical elements that are not selected by ecSql query are filtered out. By default it is 'false'.
```
<br/>

{!TransformerMetadata.md!}

{!RunningTransformation.md!}

{!Authorization.md!}

{!iModelsPermissions.md!}

{!RateLimits.md!}

---
