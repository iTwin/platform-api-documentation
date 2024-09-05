---

Run extraction of data from an iModel. This operation has two optional request body parameters: `changesetId` and `ecInstanceIds`. If `ecInstanceIds` are provided, only the ECInstances specified will be extracted. You can provide `changesetId` to run the extraction on a specific [changeset](https://www.itwinjs.org/learning/glossary/#changeset).

If you do not provide the optional request body parameters:

- latest changeset will be used for extraction
- all ECInstances will be extracted that are selected by the group queries

{!ExtractionTriggersAndConfiguration.md!}

### Notes

Data will not be extracted for a mapping if that mapping was already extracted from a newer changeset. If you wish to "go back in time" with a mapping and extract data from an older changeset, you will need to copy the mapping and run extraction on the copy.

{!Authorization.md!}

{!GroupingAndMappingPermissions.md!}

{!RateLimits.md!}

{!ExtractionRowLimiting.md!}

---
