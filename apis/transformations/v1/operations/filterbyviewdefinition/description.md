---

This endpoint is used to create a configuration for filtering iModel data based on a view definition or a saved view.

A View renders geometry from one or more Models of an iModel in a web browser. A View is an element of the ViewDefinition class. For more information, see [Using Views in iTwin.js](https://www.itwinjs.org/learning/frontend/views/).

This transformation is usually leveraged to filter out unnecessary data and align an iModel to the view within a browser window.

**Limitations**: Saved views are capable of displaying elements while hiding their parent elements. 
This cannot be achieved by filtering logic because child elements cannot exist without their parent elements within an iModel. 
To workaround this misalignment between display and filtering logic, the transformations service does not filter out:

- elements that are ancestors of visible child elements
- elements that are scoping ancestors of visible elements

Such elements will remain in iModel with cleared properties, meaning that their geometries and other non mandatory properties will be deleted.

Configuration specific properties explained:

```
models - ids of enabled/visible models contained within a view definition.
hiddenModels - ids of disabled/hidden models contained within a view definition.
categories - ids of visible enabled/categories contained within a view definition.
hiddenCategories - ids of disabled/hidden categories contained within a view definition.
neverDrawn - element ids which should be left out of the target iModel.
alwaysDrawn - element ids which should be included in to the target iModel.
isAlwaysDrawnExclusive - boolean flag that determines whether all elements, except those defined in "alwaysDrawn", should be filtered out. The default value is false if not specified.
subCategoryOvr
    - subCategory - id of sub category 
    - invisible - geometry belonging to an invisible subCategory will be left out of target iModel
clip - data needed to create clipping. This cannot be an empty object.
    - shapes - array of shape clippings
        - points - array of number arrays describing the polygon. Each low level array contains numbers corresponding to coordinates [x, y, z]
        - trans - array of number arrays describing the transform applied to the polygon. Each low level array contains four numbers of a transform row [qx, qy, qz, ax].
        - zlow - lower bound on Z.
        - zhigh - upper bound on Z.
        - mask - `true` if this shape is a mask.
        - invisible -`true` if this shape is invisible.
    - planes - array of plane line clippings
        - invisible - `true` if this union of plane clip intersections is invisible.
        - clips - a union of plane clip set intersections
            - normal - the plane's inward normal as a number array corresponding to coordinates [x, y ,z].
            - dist - the plane's distance from the origin.
            - invisible - `true` if this plane is invisible.
            - interior - `true` if this plane is interior.
perModelCategoryVisibility - array of objects containing perModelCategoryVisibility data
    - modelId - id of model for which category override will apply.
    - categoryId - id of category for which the override will apply.
    - visible - boolean flag indicating if category is visible for the given model.
viewMode - enumerator that specifies the transformation saved view mode. It can have two values: IncludeNewContent and FilterContent.
    - IncludeNewContent includes all new content that was introduced into the iModel after the view was created.
    - FilterContent filters out all new content that was introduced into the iModel after the view was created.
```

All ids must be well-formed valid hexadecimal ids conforming with [iTwin.js specification](https://www.itwinjs.org/learning/common/id64/?term=id64).

PerModelCategoryVisibility override affects geometry on all subcategories belonging to the overridden category. That is, if the category is overridden to be visible, then geometry on all subcategories of the category will be visible, regardless of any subCategory overrides.

{!TransformerMetadata.md!}

{!RunningTransformation.md!}

{!Authorization.md!}

{!iModelsPermissions.md!}

{!RateLimits.md!}

---
