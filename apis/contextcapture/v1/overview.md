# Reality Modeling API

The _Reality Modeling API_ provides the ability to turn images and point clouds into reality meshes, orthophotos and other by-products.

_Reality Modeling_ is articulated around workspaces and jobs. A _Reality Modeling_ workspace is a way to regroup similar jobs, and create gateways between jobs. A _Reality Modeling_ job is a job using basic reality data inputs (Images, point clouds) to create specified outputs (meshes, orthophotos, point clouds, orientations). Note that in order to use _Reality Modeling_, you need to already know about _Reality Management_ API (also known as _ProjectWise ContextShare_) in order to upload and download data.

On job completion, Reality Modeling emits a [realityModeling.jobCompleted.v1](/apis/webhooks-v2/available-events/#Reality%20Conversion-ref) iTwin event. Using the [Webhooks API](/apis/webhooks-v2/overview/), you can create a webhook that will be triggered by this event. On completion of a job, the endpoint specified in the webhook will be called into.
