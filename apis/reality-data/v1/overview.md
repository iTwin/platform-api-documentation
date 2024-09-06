# **This API is deprecated**

The Reality Data API is deprecated and will be removed in the future. Please use the [Reality Management API](/apis/reality-management/overview) instead.

## Shutdown date

This API was marked as deprecated on June 20th, 2023. Per [API Lifecycle](/apis/overview/lifecycle/#api-release-status) this API has entered Limited Support stage on June 20th, 2024.

We are planning to disable this API on **December 20th, 2024**.

## Reality Data API and Reality Management API differences

The Reality Management API covers the functionality of the Reality Data API and offers more. Some new features are:

- Additional filters are available when [querying](/apis/reality-management/operations/get-all-reality-data/) reality data.
- `Tags` is introduced as a new property to better identify reality data.
- `Classification` property becomes optional on creation of reality data.

The breaking changes are as follows:
- The `itwin-platform` scope should cover all needs to access reality data in read or write mode.
- `iTwinId` parameter is introduced and replaces `projectId`. This affects all operations.
- The reality data creation payload changes. `iTwinId` property is also moved in as a property inside the reality data body payload. Pay attention to the new structure of the reality data body payload. See [reality-management](/apis/reality-management/operations/create-reality-data/#request-body) documentation.
- Getting [Read](/apis/reality-management/operations/get-read-access-to-reality-data-container/) or [Write](/apis/reality-management/operations/get-write-access-to-reality-data-container/) container access is now split in two separate endpoints.

## How to use Reality Management API
To use the Reality Management API please specify `Accept: application/vnd.bentley.itwin-platform.v1+json` header with all the requests to [https://api.bentley.com/reality-management](https://api.bentley.com/reality-management) API. The [Reality Management tutorials](/apis/reality-management/tutorials/) provide further guidance.

Using the `itwin-platform` scope should be sufficient for any app. Make sure you review the scopes in your [Apps](/my-apps/).

If your application is using the `@itwin/reality-data-client` package, it should be updated to use version 1.1.0 or greater but it is recommend you update to the latest possible version. Note that the package has moved to the [reality-capture repository.](https://github.com/iTwin/reality-capture/tree/main/typescript/packages/reality-data-client)
- [@itwin/reality-data-client](https://www.npmjs.com/package/@itwin/reality-data-client) 

# Reality Data API

Reality modeling is the process of capturing the physical reality of an infrastructure asset, creating a representation of it, and maintaining it through continuous surveys. Reality models add real-world digital context to infrastructure projects. The Reality Data API provides the ability to retrieve information about the reality data that is associated with an infrastructure project.

## RealityData

The class defines properties that describe the content of the reality data and provides an access point to the data stored in a blob container, using Microsoft Azure Storage technologies. RealityData properties represent the descriptive data related to a reality data. In addition to this, reality data content is stored as files and folders within a blob container uniquely associated to this reality data. Individual files and folders follow, from the root of the reality data, a normal file tree structure.

A more detailed documentation on RealityData properties is available [here](/apis/reality-data/rd-details/).

## Projects

RealityData are bound to Projects. Projects are used to represent engineering projects for an infrastructure asset. iModels, reality data, and engineering documents can be associated with a project. The iTwins API is used to create or query project iTwins [See more information about the iTwins API here](/apis/itwins/overview/). The Access Control API is used to manage project team members and project roles [See more information about the Access Control API here](/apis/access-control-v2/overview/).