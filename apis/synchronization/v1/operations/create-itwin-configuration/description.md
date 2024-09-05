---

Create a configuration that defines how data is processed and synced to iModels in the specific iTwin.

### Configurations

#### uploadDgnRealityData

Enables reality data upload to Reality Data API while synchronizing files to iModels, if .3sm, .3mx, .pod, or raster attachments are attached to CAD data.
The default value is true.

Having this configuration set to true will trigger credit usage for Reality Data service.

#### convertDgnTerrainModels

Enables terrain model elements to be processed during dgn-based synchronizations.
The default value is false.

#### squashIntermediateRevisions

Enables the creation of a single Changeset for physical and drawing elements (2D, 3D) coming from all Source Files. Separate Changesets will be pushed for any schema or definition changes.
The default value is false.

Use case example: minimize a linear timeline of the iModel changes. However, in this case, you would not be able to get information on individual Source File changes.

#### convertDgnHyperModelingSections

Enables displaying the 2D section graphics and annotations in the context of the 3D model.
The default value is true.

Use case example: typical design files include hypermodels, and the intent is to expose such information in a viewer. Refer to the sample of how to navigate between the 2D and 3D views easily: [sample](https://www.itwinjs.org/sandboxes/iTwinPlatform/Hyper-modeling) 

#### skipRvtReprojection

Ignores geo-location defined in .rvt file and overlaps the model at the local iModel coordinates.
The default value is false.

This configuration will have no effect if Revit was the first file synchronized to an empty iModel.

Use case example: multiple Revit files will need to be synchronized; if individual files are not aligned to the exact location, this configuration will bring all the models to the same place. However, we suggest enhancing the original design files with proper geographic coordinate systems before synchronization instead of using this configuration.

{!Authorization.md!}

---
