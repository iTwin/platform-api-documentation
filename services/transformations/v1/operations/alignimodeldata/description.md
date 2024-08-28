---

This endpoint is used to create a configuration for align iModel data transformation.

Align iModel data transformation provides the capability of remapping element EClasses and their ECProperties, and performing modifications on **dynamic** ECSchemas. Dynamic schema modifications include the removal of unused ECClasses and merging multiple ECClasses into a single ECClass.

Configuration specific properties explained:

```
schemaOptimizationOptions - options that will modify ECSchemas.
    - removeUnusedClasses - if `true` ECClasses that have 0 elements will be removed from all **dynamic** ECSchemas.
    - classMergingGroups - array of ECClass merging group objects.
        - sourceECClasses - array of ECClass objects. Classes in this array will be merged into a single target ECClass. All class elements will also be remapped into the target ECClass.
            - ecClassName - ECClass name.
            - ecSchemaName - ECSchema name.
        - targetECClass - target ECClass. all sourceECClasses will be merged into this ECClass.
            - ecClassName - ECClass name.
            - ecSchemaName - ECSchema name.
dataRemappingOptions - options for data remapping.
    - additionalECSchemas - array of Bentley defined ECSchemas that will be imported into the target iModel
        - ecSchemaName - ECSchema name.
        - ecSchemaVersion - ECSchema version.
    - elementGroups - array of element group objects. Each object in the array defines a collection of elements to be mapped into a single target ECClass.
        - targetECClass - a target class for the elements selected by the `elementPropertyQuery` to be remapped into.
            - ecClassName - ECClass name.
            - ecSchemaName - ECSchema name.
        - elementPropertyQuery - ECSql query that selects element ECInstanceIds and any additional properties.
```

### Target ECClass

If `targetECClass` does not exist in the source iModel its schema must be imported using the `additionalECSchemas` property.

### Element Property query

The `elementPropertyQuery` must be a valid ECSql statement. The only requirement for the query is that it must select ECInstanceId column. Elements with these ids will be remapped into the `targetECClass`. Any additional column the query returns is treated as an additional property. Given that the additional property's column name and an ECProperty in the `targetECClass` name match, its value will be carried through and will be exported as that ECProperty's value in the target iModel. Column names for ECProperties are case insensitive.

#### Example

`ArchitecturalPhysical.Door` ECClass has 3 ECProperties defined - `OverallHeight`, `OverallWidth` and `Description`. To remap all `Generic.PhysicalObject` elements that have "door" in their UserLabel to an `ArchitecturalPhysical.Door` ECClass, a valid `elementPropertyQuery` would be:
- `SELECT ECInstanceId, 'This element was remapped from PhysicalObject' as Description, 15 as OverallHeight FROM Generic.PhysicalObject WHERE UserLabel LIKE '%door%'`

Remapped elements in the target iModel would have the following properties:
- Description: 'This element was remapped from PhysicalObject'
- OverallHeight: 15
- OverallWidth: NULL
- ...

Original properties will be carried through from the original element and any properties that do not exist in the target class will be lost.

To change already existing element property, select an already existing column. The following query will change all `BisCore.PhysicalObject` class element's user labels to 'Updated user label':
`SELECT ECInstanceId, 'Updated user label' as UserLabel FROM Generic.PhysicalObject`

{!TransformerMetadata.md!}

{!RunningTransformation.md!}

{!Authorization.md!}

{!iModelsPermissions.md!}

{!RateLimits.md!}

---
