---

This endpoint is used to create a configuration for a CreateFork transformation.

CreateFork transformation is used for establishing a (*main <-> fork*) relationship between 2 iModels and for synchronizing changes in the "forward" (*main -> fork*) direction.

The first time a CreateFork transformation is performed, a link is established between source (main) and the target (fork) iModels. The target iModel must be a clone of the source iModel. You can clone the existing iModel using iModels API's endpoints:
- [Create iModel](/apis/imodels-v2/operations/create-imodel/). 
- [Clone iModel](/apis/imodels-v2/operations/clone-imodel/). 

Consecutive CreateFork transformations may be used to pull changes from the main iModel into the fork iModel.

To synchronize changes in the "reverse" (fork -> main) direction see [MergeFork configuration](/apis/transformations/operations/mergefork/).

{!TransformerMetadata.md!}

**Limitations**: Since an iModel can contain multiple forks there is a possibility that any given fork and the main iModel end up with conflicting schemas, e.g., the same ECProperty in one schema is of type "number" and in another schema it is of type "string". Schema conflicts are not handled by the transformations service and in these cases the transformation will fail.

{!RunningTransformation.md!}

{!Authorization.md!}

{!iModelsPermissions.md!}

{!RateLimits.md!}

---
