---

This endpoint is used to create a configuration for filtering out geometry entries based on their sub-category names.

A SubCategory is a subdivision of a Category. SubCategories allow elements in iModel to have multiple pieces of geometry that can be independently visible and styled (color, linesStyle, transparency, etc.). For more information, see [SubCategories](https://www.itwinjs.org/bis/intro/categories/#subcategories).

FilterSubCategories transformation is filtering out all of the data associated to subCategoryNames specified for the transformation.

Configuration specific properties explained:

```
subCategoryNames - array of sub category names.
```
<br/>

{!TransformerMetadata.md!}

{!RunningTransformation.md!}

{!Authorization.md!}

{!iModelsPermissions.md!}

{!RateLimits.md!}

---
