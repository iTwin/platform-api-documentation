---

This endpoint is used to create a configuration for Merge iModel transformation.

Merge iModel transformation is used for synchronizing changes between fork and main iModels in either direction.

Merge iModel transformation should be used to synchronize changes between main and fork iModels created using ["Fork iModel" operation in iModels API](/apis/imodels-v2/operations/fork-imodel/) whereas [Merge Fork](/apis/transformations/operations/mergefork) should be used with forks created using one of
[Create Fork](/apis/transformations/operations/createfork), [Filter IModel](/apis/transformations/operations/filterimodel), [Filter SubCategories](/apis/transformations/operations/filtersubcategories), [Filter By View Definition](/apis/transformations/operations/filterbyviewdefinition) transformations.

{!RunningTransformation.md!}

### Merge iModel transformation requirements

iModel fork must be created using [Fork iModel operation](/apis/imodels-v2/operations/fork-imodel/) in iModels API. Additionally, all elements in both fork and main iModels must have `FederationGuid` property set to a non `null` value. If that is not the case, [PopulateFederationGuids transformation](/apis/transformations/operations/populatefederationguids/) can be used to set missing `FederationGuid` values.

### Merge direction

Source and target (project & iModel) properties mark the data flow direction:

- If `sourceIModelId` is iModel **fork** and `targetIModelId` is **main** iModel, it means that iModel fork is being merged to main iModel.
- If `sourceIModelId` is **main** iModel and `targetIModelId` is iModel **fork**, it means that main iModel is being merged to iModel fork.

Running consecutive transformations for this configuration will keep synchronizing newly added changes in the specified direction.

### Transformation state persistence in iModel fork

In addition to exported data, the transformer will also push some additional metadata to iModel fork. This metadata contains:

1. `BisCore:RepositoryLink` and `BisCore:ExternalSource` elements that mark the source where the data was imported from.
1. A "Scope" `BisCore:ExternalSourceAspect` that contains Synchronization changeset metadata that is needed by the transformation service to process any later changes correctly.

{!Authorization.md!}

{!iModelsPermissions.md!}

**Important**: Merge iModel transformation is in closed preview mode currently and only selected applications can utilize it.

{!RateLimits.md!}

---
