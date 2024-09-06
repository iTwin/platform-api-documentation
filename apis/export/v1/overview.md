## Export

The Export API provides the ability to export engineering data from an iModel to different standard formats like 'IFC' or 'LandXML'. With this API, you can start exporting from an iModel and with a job run, the output file will be stored against the projectId provided. To get the file generated use Storage API.

The API supports following export types:

- IFC (IFC versions supported - 'IFC4.3' (IFC4.3_ADD2), 'IFC2x3', 'IFC2x3 CV 2.0', 'IFC4 RV 1.2').
- LandXML.

Note: Support for 'LandXML' export has been removed for now.

To create and run an export:
  1. Create an export connection.
  2. Run the created connection by passing the necessary information.
  3. Get the run status.

### Connection

The export process is based on connections that establish links to iModels. For example, there could be multiple connections for an iModel, and those executed on-demand multiple times to continuously export changes. The history of runs is preserved and available for monitoring.

### Run

A run defines a single connection export process. Initialize the run by sending a run start request. This entity has properties like status, duration, and others. There can be only one run per connection at a time.

### Authorization

The export process usually takes time and is performed in the background. For that, we need to store the user's refresh token. The refresh token needs to be stored before calling the 'Create ExportConnection Run' end-point. You can get authorization information by using [Get Authorization Information API](/apis/export/operations/get-authorization-information/). This API will return the current status and a redirect URL if the token has to be renewed.