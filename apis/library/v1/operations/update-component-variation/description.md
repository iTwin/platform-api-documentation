---

Updates a component variation in user's organization context.

### Notes

To update a variation request body must contain all the properties desired for the variation since this will replace existing variation with current variation definition. DisplayName is required property. If variation contains AdHocProperties, displayName and type are required properties of AdHocProperty.

AdHocProperty type values are:
-StringType
-IntegerType
-DoubleType
-FloatType
-BooleanType

{!Authorization.md!}

{!LibraryPermissions.md!}

{!RateLimits.md!}

---