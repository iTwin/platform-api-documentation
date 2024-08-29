---

Use this endpoint to create CombinePhysicalModelsV2 configuration.

Combine Physical Models V2 transformation combines models in source iModel based on the EC query into target physical models with specified names. It is mandatory to only create source model queries which select ECInstanceId by using `*` or explicitly selecting that column. Also, source queries must pick only physical models that are sub-modeling physical partition.
For more information about internal iModel structure, see [Example Information Hierarchy](https://www.itwinjs.org/bis/guide/data-organization/information-hierarchy/#example-information-hierarchy).

This transformation allows to optimize iModel for better viewing performance. You can notice lack of performance when model count reaches ~1000 or even more models.
You can select ~ 5-20 models by EC query and test the performance of the iModel.

Explanation of specific properties configuration.
```
modelGroups - property specifies an array of target model names with source model queries that you want to transform. This property is required.
groupUnselectedModels - optional parameter which indicates your decision on grouping unselected models. Default value is false.
unselectedModelsGroupName - optional parameter which sets name for unselected models group. You must specify the name if groupUnselectedModels is true.
simplifyGeometry - optional parameter indicating if geometry simplification should be used (transforming parasolids to meshes). Default if not specified - false.
```
<br/>

{!TransformerMetadata.md!}

{!RunningTransformation.md!}

{!Authorization.md!}

{!iModelsPermissions.md!}

{!RateLimits.md!}

---
