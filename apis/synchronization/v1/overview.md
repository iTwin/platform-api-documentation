## Synchronization

The Synchronization API provides the ability to aggregate, align and synchronize engineering data from different formats to an iModel. With this API, you can set up a connection with various source files and, with a job run, synchronize those to an iModel. Requests will be processed in a cloud using associated iTwin connectors.

The API offers the following:

- iTwin connectors for various design applications and interchange formats. See the complete list in [supported formats section](/apis/synchronization/supported-formats/).
- File synchronization from [iTwin Storage service](/apis/storage/). Use the [Synchronization Storage](/tutorials/synchronization-storage-tutorial/) tutorial and provided sample [Synchronize File from Storage](https://github.com/iTwin/synchronization-api-sample-app) to help you get started.
- File synchronization from pre-authenticated urls. Use the [Synchronization Manifest](/tutorials/synchronization-blob-tutorial/) tutorial and provided sample [Synchronize Files from Azure Blob or SharePoint](https://github.com/iTwin/synchronization-manifest-api-sample) to help you get started.
- Set required synchronization configuration on iTwin, iModel, or Connection scopes. Use the [Configuration](/tutorials/synchronization-configurations-api-tutorial/) tutorial as a guide.<TechPreviewBadge style="margin-left:8px; position:relative; bottom:1px"/> **Technical Preview.**
  <img src="/documentation/synchronization/SynchronizationManifestDiagram.PNG" alt="iTwinSynchronizerSteps" title="iTwin Synchronizer Steps" style="width:70%"/>

To create and run initial synchronization:

1. Create a manifest connection
2. Get pre-authenticated file access URLs
3. Run created connection by passing access URLs
4. Get the run status

To update an iModel when engineering data is changed:

2. Get pre-authenticated file access URLs
3. Run created connection by passing access URLs
4. Get the run status

### Connection

The synchronization process is based on connections that establish links from design files to iModels. For example, there could be multiple connections for an iModel, and those executed on-demand multiple times to continuously synchronize changes. The history of runs is preserved and available for monitoring.

### Source File

A source file entity defines the link between a specific file in the data source and iTwin connector during the synchronization run. Mark the source file as a spatial root if file has geographical coordinate information.

### Run

A run defines a single connection synchronization process. Initialize the run by sending a run start request. This entity has properties like status, duration, and others. There can be only one run per connection at a time.

### Connector

An iTwin Connector will process a file from an application such as MicroStation and transform the model's content (geometry, properties, and relationships) into an iModel. It will also include creating a schema from the source data. You can synchronize several models using the same Connector or different models using various Connectors to achieve the required iModel.

iTwin Connectors detect the differences in the source models between job runs. The synchronization will produce [Changesets](/apis/imodels-v2/) – which contain the changes sent to iModelHub. This is the critical difference between a Connector and a one-time converter.

The first time you run the synchronization, the Changeset will contain the content of the entire model. Subsequent synchronization runs create Changesets for the incremental differences between what previously existed in the iModel and your changes. The iTwin Connector will not process the synchronization if there are no source model changes. In this case, no Changesets are pushed.

### Authorization

The synchronization process usually takes time and is performed in the background. So there are two ways to call the API:

- If the application is centered around the user and has user interface, user authorization workflow can be used. For that, we need to store the connection owner's refresh token. You can get it by using [Get Authorization Information API](/apis/synchronization/operations/get-authorization-information/). If the token needs to be renewed, this API returns the current status and a redirect URL.
- If the application does not have a user interface and synchronization will be initiated by a backend service, then service type application should be used and authenticationType: "Service" should be set on a connection.

### Media Links

Additional information can be found here:

- The Synchronization API - [Accreditation course](/learning/courses/synchronization-api/course-intro/course-intro/)
- iTwin Developer Conference 2022. Synchronization API: Connectors to the Rescue - [YouTube](https://www.youtube.com/watch?v=ZJ16KIrNPZU)
- iTwin Developer Webinar. iTwin Synchronization: Bring Together a Wide Array of Disparate Engineering Data - [YouTube](https://www.youtube.com/watch?v=M0X94XQBahY)
