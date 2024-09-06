# Reality Conversion API

The _Reality Conversion API_ provides the ability to convert reality files such as point clouds from [supported source format](#supportedconversiontypes) to [supported target format](#supportedconversiontypes). Point clouds produced by scanning devices are often stored in large files, in a format that reflects to the way data is captured but that is not ready to be directly consumed interactively in a web viewer. One of the main purposes of such a conversion is to make reality data, when stored in a non-web-friendly format, ready for web consumption.

Once a Reality Conversion job is completed, it emits a [realityConversion.jobCompleted.v1](/apis/webhooks-v2/available-events/#Reality%20Conversion-ref) iTwin event. Using the [Webhooks API](/apis/webhooks-v2/overview/), you can create a webhook that will be triggered by this event. On completion of a job, the endpoint specified in the webhook will be called into.

##Input
One or more reality data containers with correct classification and type, each hosting one or more files.
All files processed in one conversion operation must have the same format.

##Output
One reality data container with the requested type.
Depending on the use of the `merge` option, the output reality data will host only one file (merge), or one per input file (no merge).
In the latter case, if several files from several input containers have the same name, only one of them will be processed in the conversion operation. For instance, if reality data container C1 contains two files, named fileA.las and fileB.las, and reality data container C2 contains one file named fileA.las, the output of conversion of C1 and C2 to OPC without merge will contain only 2 files: fileA.opc and fileB.opc. Only fileA.las from container C2 (last in alphabetical order) will be converted, the other file with the same name will be ignored.

##Supported data formats
The table below lists all the formats supported as input or output. Conversions can be run for any combination of one input and one output format.

|      File Format       | File Extension | Reality Data Type | Input | Output |
| :--------------------: | :------------: | :---------------: | :---: | :----: |
|        ASTM E57        |      .e57      |        E57        |  \*   |        |
| Laser Exchange Format  |      .las      |        LAS        |  \*   |        |
| LASzip Exchange Format |      .laz      |        LAZ        |  \*   |        |
|  Polygon File Format   |      .ply      |        PLY        |  \*   |        |
|   Orbit Point Cloud    |      .opc      |        OPC        |       |   \*   |
| Cesium 3D Point Cloud  |    .3dTiles    |       PNTS        |       |   \*   |
