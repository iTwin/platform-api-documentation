## iModels OData

Access iModel data using an OData interface.

### Mapping

The iModels OData API allows accessing iModels data in the view of Reporting API [Mappings](/apis/insights/overview/) without running the [Extraction](/apis/insights/operations/run-extraction/) process.

Note: Not all Mapping configuration options are supported in this API.

### Use cases

This API should be used in embedded views where only partial data is fetched. Follow the [Customizing the iTwin Viewer](/tutorials/itwin-viewer-hello-world/) tutorial on how to integrate it into iTwin Viewer.

Use the Reporting API [Extraction](/apis/insights/operations/run-extraction/) process for full data exports.

### OData

OData APIs can be used with tools and libraries that support [OData v4 protocol](https://www.odata.org/documentation/) and [OAUTH2 Authorization](/apis/overview/authorization/).

## Client Packages

To read the OData endpoint [OData Library](https://www.odata.org/libraries/) is needed.

## Media Links

Additional information can be found here:

* Creating and Sharing Insights with the iTwin platform - [YouTube](https://www.youtube.com/watch?v=6MhEm6cTOqY)
* Decluttering your Digital Twin - [Medium](https://medium.com/itwinjs/decluttering-your-digital-twin-9000bd017f50)