---

Returns Checkpoint associated with the provided Named Version. Checkpoint is a pre-processed iModel baseline file that has changes up to a certain Changeset already applied and is stored on the server. This can be used to reduce number of Changesets needed to apply to get to a certain version of the iModel.

A Checkpoint is generated when a Named Version is created for that changeset.

Checkpoint can be stored in two different ways:
1. `download` property will have a Azure Blob storage link to a full `.bim` file that has changes applied up to the Changeset specified by `changesetIndex` and `changesetId` properties.
2. `containerAccessInfo` will have an access key to Azure Blob container that stores the Checkpoint in 4 MB blocks. **Important: This property should only be used by iTwin.js libraries.**

A successfully generated Checkpoint will have one or both of these properties.

{!Authorization.md!}

{!iModelsPermissions.md!}

{!RateLimits.md!}

---
