---

Creates a mapping for an iModel. There are two ways to create a mapping.

### Create an empty mapping

To create an empty mapping do not provide the `sourceMappingId` property. This will create a new mapping that does not have any groups.

### Create a mapping from an existing mapping

To create a mapping from another mapping provide the `sourceMappingId` property. The server will create a new mapping and copy over all of the groups with their properties from the mapping referenced by the `sourceMappingId` property. User must have `imodels_read` permissions to the iModel containing the source mapping. Changing source mapping, groups, or their properties will not change the copies of them.

Provided `mappingName`, `description`, `extractionEnabled` request body properties will overwrite the properties on the copied mapping.

{!Authorization.md!}

{!GroupingAndMappingPermissions.md!}

{!ExtractionTriggersAndConfiguration.md!}

{!RateLimits.md!}

{!ExtractionRowLimiting.md!}

---
