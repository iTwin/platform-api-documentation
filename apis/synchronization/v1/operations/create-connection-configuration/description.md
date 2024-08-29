---

Create a configuration that defines how data is processed and synced to iModels with the specific connection.

### Configurations

#### reclassifyDgnElements

Enables connector to change the base class of an element if its current classification comes from the Generic schema.
The default value is false.

If this configuration is set to true:

- Every Generic element in the model will be re-processed, so expect a longer synchronization job.
- Elements that are derived from a BIS class will not be processed.
- Elements that did not change in the source file may appear modified in iModel if you use the Changed Elements API.
- Elements that changed will appear deleted and added in iModel if you use the Changed Elements API.
- Suggest setting this configuration with caution and per required run basis, not perpetual.

Use case example: If you have been advised by Bentley support that the Connector has added additional support for your files' disciplines (e.g. additional BIS schema alignment), then this option should be enabled on the next run to opt-in to the updated alignment.

#### ignoreDgnAttachments

Enables skipping of all reference attachments. As a result, only the master file is synchronized into the iModel. Only applicable for .dgn and .dwg files.
The default value is false.

A reference file could have a transform/ level override/ symbology override when attached through a master file. None of these settings will be available if the files are processed individually and could result in data not matching the intended design.

#### enableSheetsAndDrawings 

Controls sheets and drawings synchronization. If enabled all sheet models and relayed drawings will be synchronized to an iModel.
The default value is false.

#### enableC3dGraphsIn2dModel

Enables the separation of 2D elements from 3D elements in the target iModel when using Civil Connector. The 2D elements will be inserted into a graph model, while the 3D elements will be kept in the spatial model. The default value is false.

Standard AutoCAD 2D entities, such as MTEXT, LINE, POLYLINE, etc., laid on the XY plane in the model space, will be converted as 2D elements and inserted into the graph model. This feature flag does not impact alignments and their labels, which always stay in the spatial model.

If the file contains only AutoCAD entities and no Civil3D entities or has Civil3D model entities but no 2D graphics, we suggest leaving this configuration as false.

#### enableSheetIndex

A sheet index is a centralized and structured collection of sheets in your WorkSet. Enabling this flag triggers processing of sheet index files from the associated workspace.The default value is false.

Use case example: Sheet index can be useful in creating a construction document set. So a civil user might be interested in turning on this flag to get the content of the sheets he has configured.

#### filterBySheetIndex

A sheet index is a centralized and structured collection of sheets in your WorkSet. Enabling this flag limits (filters) the processing of sheets provided to the connector to the ones specified in the sheet index. The default value is false.

Use case example: Sheet index can be useful in creating a construction document set. However, there could be large number of sheets present in the input set and the user may be only interested in the ones specified by the sheet index. Enabling this flag allows such filtering.
{!Authorization.md!}

---
