---

This endpoint is used to create a configuration for an ImportIModel transformation.

Import iModel transformation imports an iModel from source project to specified target.

Multiple iModels may be imported into the same target iModel, effectively combining them.

Element conflicts can occur when importing an iModel. In this case, elements of the iModel being imported overwrite the target elements. Only elements whose scoping hierarchy ultimately reaches elements with ids `0x10` (dictionaryId) and `0xe` will be able to conflict with each other (most common cases are `DefinitionElement`s).

{!TransformerMetadata.md!}

{!RunningTransformation.md!}

{!Authorization.md!}

{!iModelsPermissions.md!}

{!RateLimits.md!}

---
