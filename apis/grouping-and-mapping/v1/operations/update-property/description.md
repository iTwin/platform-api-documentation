---

Updates a property. If group is a table, then property of that group is a column. Properties can be mapped from existing iModel ECProperties, calculated using a predefined list of calculations, or calculated using your own mathematical formula.

Source of the property value in the output is defined by the `ecProperties`, `calculatedPropertyType`, and `formula` values on a property. You can provide any combination of these properties. If you do not provided any of them, the output value will always be null. Such properties can be used as placeholders or to define an output schema before any property mapping is done. However, when you provide 2 or more of these properties they are evaluated in this order until a valid value (not null or undefined) is found:

1. `ecProperties`
2. `calculatedPropertyType`
3. `formula`

Property values are assigned during data extraction. To start the data extraction use [Run Extraction](/apis/insights/operations/run-extraction) operation.

{!MappingECProperties.md!}

{!CalculationTypes.md!}

{!CustomCalculations.md!}

{!Authorization.md!}

{!GroupingAndMappingPermissions.md!}

{!RateLimits.md!}

{!ExtractionRowLimiting.md!}

---
