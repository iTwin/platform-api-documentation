---

Create a configuration that defines how data is processed and synced to iModels in the specific iModel.

### Configurations

#### clampZExtent

Enables a limit for the project Z extent maximum up to Mount Everest height (i.e.8849 meters). Works only when project extent in XY direction is defined for iModel.
The default value is false.

Display performance can be adversely affected if source data is poorly aligned or contains elements far from the project's physical location. If files cannot be corrected, this configuration would help viewers to restrict the Z extent.

Use case example: allows restricting viewport to the bounding box so that any arbitrary geometry far away from the actual design does not impact fitting the model to the viewport.

#### overrideRvtReprojectionDistance

Define distance in meters when to start ignoring .rvt file geo-location data and reprojecting graphics based on local iModel coordinates.
The default value is 0.

Reprojection happens when the .rvt file and iModel have different geographic coordinate systems. If the distance between both GCS is bigger than the number provided with the flag, reprojection will be skipped, and no errors will be reported. Otherwise, reprojection will be applied.
This configuration will have no effect if Revit was the first file synchronized to an empty iModel.

Use case example: no reprojection of Revit file is needed beyond some pre-defined radius.
{!Authorization.md!}

---
