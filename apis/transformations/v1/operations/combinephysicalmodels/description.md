---

This endpoint is used to create Combine Physical Models configuration.

Combine Physical Models transformation combines the source iModel's top level hierarchy physical models to a desired amount of models.
For more information see [iModel Information Hierarchy](https://www.itwinjs.org/bis/guide/data-organization/information-hierarchy/#example-information-hierarchy).

This transformation is usually leveraged to improve performance of iModel viewers. Lack of performance is noticeable when model counts reach ~1000 or even more models.
It is recommended you set the `numberOfModels` property to ~ 5-20 and test the performance of the iModel.

Configuration specific properties explained:
```
numberOfModels - specify amount of models to transform the source iModel into.
simplifyGeometry - optional parameter indicating if geometry simplification should be used (transforming parasolids to meshes). Default if not specified - false.
```
<br/>

{!TransformerMetadata.md!}

{!RunningTransformation.md!}

{!Authorization.md!}

{!iModelsPermissions.md!}

{!RateLimits.md!}

---
