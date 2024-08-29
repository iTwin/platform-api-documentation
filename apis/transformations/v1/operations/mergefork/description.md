---

This endpoint is used to create a configuration for MergeFork transformation.

MergeFork transformation should be used for synchronizing changes in the "reverse" (*fork -> main*) direction with Forks created using one of
[CreateFork](/apis/transformations/operations/createfork), [FilterIModel](/apis/transformations/operations/filterimodel), [FilterSubCategories](/apis/transformations/operations/filtersubcategories), [FilterByViewDefinition](/apis/transformations/operations/filterbyviewdefinition) transformations. Forks created using ["Fork iModel" operation in iModels API](/apis/imodels-v2/operations/fork-imodel/) should be synchronized using [MergeIModel](/apis/transformations/operations/mergeimodel) transformation.

Forked iModel must have at least one new changeset with modifications for merging to succeed.

Source and target (project & iModel) properties mark the data flow direction. That said MergeFork configuration's sourceProjectId/IModelId and targetProjectId/IModelId properties must be switched places as compared to the configuration that was used to fork the iModel.

```json
{
    "sourceProjectId": "00000000-0000-0000-0000-000000000000", // forked iModel's project id
    "sourceIModelId": "00000000-0000-0000-0000-000000000000",  // forked iModel's id
    "targetProjectId": "00000000-0000-0000-0000-000000000000", // main iModel's project id
    "targetIModelId": "00000000-0000-0000-0000-000000000000",  // main iModel's id
    "transformParameters": {
        "configurationId": "00000000-0000-0000-0000-000000000000" // id of a configuration that was used to create the fork
    }
```

Explanation of specific properties configuration.
```
configurationId - required property that specifies configuration id, which was used to fork the main iModel.
```
<br/>

Running consecutive transformations for this configuration will keep synchronizing newly added changes from fork iModel back into the main iModel.

{!TransformerMetadata.md!}

Differently from other transformation types, MergeFork transformation synchronizes changes in a "reverse" direction. This means that the metadata will be pushed to the source (fork) iModel instead of the target iModel.

**Limitations**: Since an iModel can contain multiple forks there is a possibility that any given fork and the main iModel end up with conflicting schemas, e.g., the same ECProperty in one schema is of type "number" and in another schema it is of type "string". Schema conflicts are not handled by the transformations service and in these cases the transformation will fail.

{!RunningTransformation.md!}

{!Authorization.md!}

{!iModelsPermissions.md!}

{!RateLimits.md!}

---
