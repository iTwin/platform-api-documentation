---

This endpoint is used to create CombineIModels configuration.

Combine IModels transformation combines the source iModel with iModels provided in transformation parameters.
This is done by importing each source iModel into the target iModel sequentially. IModels are imported into the target in the same order that they were provided in (`configuration.sourceIModel`, `configuration.transformParameters.iModels[0]`, `configuration.transformParameters.iModels[1]`, etc.).

For every source iModel a `BisCore:Subject` is created in the target iModel. Each source iModel's contents are exported under their corresponding subject in the target. Subjects are named after their source iModels. Any possible naming conflicts are resolved by appending a number to the subject's name if needed (ex. `Duplicate name 2`).

Also, a new definition partition is created under new subject to persist all ViewDefinitions from source iModels, even if they have conflicting codes. This means that all ViewAttachment, ViewDefinition, ModelSelector, DisplayStyle and CategorySelector elements that are scoped under the dictionary model (id '0x10'), will be remapped under this newly created definition partition.

Element conflicts can occur when merging iModels (e.g. 2 subCategories with the same Element Code have different appearance props).
In this case, every iModel in the import chain will keep overwriting the conflicting element effectively preserving the last value that was found. This means that the last iModel in the `transformParameters.iModels` list will take precedence.
Only elements whose scoping hierarchy ultimately reaches elements with ids `0x10` (dictionaryId) and `0xe` will be able to conflict with each other (most common cases are `DefinitionElement`s). Any other elements that are ultimately scoped by the root subject will be imported under a new subject as mentioned above and cannot conflict (because their scope becomes unique).

The first Geo location that is found will be applied onto the target iModel.
For example, if merging three iModels in this order:

1. `iModel A` (not geo located)
2. `iModel B` (geo location is `BB`)
3. `iModel C` (geo location is `CC`)

Target iModel will have geo location set to `BB`.

Configuration specific properties explained:
```
iModels - list of iModels to combine the source iModel with.
    - iModelId - id of iModel
    - projectId - id of project that iModel belongs to
```
<br/>

**Limitations**: This API does not support combining iModels that have conflicting dynamic ECSchemas.
Conflicting ECSchemas are two ECSchemas that have the same name, but have at least one difference such as:
 different aliases or any difference between EC object items ([EC schema contents](https://www.itwinjs.org/bis/ec/)).
 For example, "CustomSchema" in iModel "A" has an ECClass "MyClass", while "CustomSchema" in iModel "B" doesn't have
 an ECClass "MyClass".

In case of ECSchema conflict, transformation will fail with an error message. Those error messages
might vary depending on the conflict that was encountered. Transformation status and 
it's error message can be retrieved by sending 
[GET transformation](/apis/transformations/operations/get-transformation/) request.

{!TransformerMetadata.md!}

{!RunningTransformation.md!}

{!Authorization.md!}

{!iModelsPermissions.md!}

{!RateLimits.md!}

---
