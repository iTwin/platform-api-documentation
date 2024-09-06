# Reality Analysis API

The _Reality Analysis API_ provides the ability to run Artificial Intelligence / Machine Learning (AI/ML) on photos, maps, meshes or point clouds. It can detect objects or features in 2D and 3D for defect analysis, image anonymization, image indexing, asset management, mobile mapping, aerial surveying, and more.

_Reality Analysis_ is articulated around _Reality Data_ and _Jobs_. Reality Data are the data be to analyzed (photos, maps, meshes or point clouds). To describe on which data the analysis should be run and potentially some extra metadata (e.g. photo positions), we introduce a new type of Reality Data named _ContextScenes_. The analysis usually requires one or more Machine Learning models (e.g. a deep learning neural network). We call them _ContextDetectors_.
Given ContextScenes and ContextDetectors, a Reality Analysis job produces different kinds of annotations (e.g. detected objects), which we store again in a ContextScene.

Once a Reality Analysis job is completed, it emits a [realityAnalysis.jobCompleted.v1](/apis/webhooks-v2/available-events/#Reality%20Analysis-ref) iTwin event. Using the [Webhooks API](/apis/webhooks-v2/overview/), you can create a webhook that will be triggered by this event. On completion of a job, the endpoint specified in the webhook will be called into.

All the above mentioned reality data are stored via the Reality Management Service. The rest of the presentation assumes that you are familiar with the [Reality Management API](/apis/reality-management).

The [tutorials](/apis/realitydataanalysis/tutorials/) and [samples](/apis/realitydataanalysis/samples/) are good places to start using Reality Analysis, as well as the [API Reference](/apis/realitydataanalysis/operations/). Before we recommend reading:

- The [Context Scene](/apis/realitydataanalysis/rda-cs/) description.
- What a [Context Detector](/apis/realitydataanalysis/rda-cd/) is.
- An overview of the different Reality Analysis [job types](/apis/realitydataanalysis/rda-jobtypes/).
- [Python and TypeScript SDKs and samples](https://github.com/iTwin/reality-capture/) to use iTwin Capture services.
