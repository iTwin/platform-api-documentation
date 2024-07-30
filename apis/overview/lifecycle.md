<!-- Copyright (c) Bentley Systems, Incorporated. All rights reserved.            -->
<!-- See LICENSE in the project root for license terms and full copyright notice. -->

# API versioning and release lifecycle

## API versions

We version all APIs and embeds the version number in the **Accept** header as shown below.

```HTTP
GET https://api.bentley.com/users/me HTTP/1.1
Authorization: Bearer JWT_TOKEN
Accept: application/vnd.bentley.itwin-platform.v1+json
```

We are continually improving our APIs and increment the API version number when we introduce a breaking change. A breaking change is a non-backward compatible change in the API that can cause applications using the API to no longer function as expected. The following are examples of changes that are not backward compatible:

- Changing the URI of the resource
- Changing the method used to access a resource
- Adding new required request parameters
- Changing a field name or deleting a field from the response

The following changes are backward compatible:

- Adding new API endpoints
- Adding new optional request parameters
- Adding new fields to the response

As much as possible, we will notify you of a breaking change well before its release. When we release a new version of an API, we provide one year for you to update your applications. The exact amount of notice we provide may vary depending on why the breaking change is necessary.

## API release status

API product releases have a well-defined lifecycle. The release status determines the level of support we offer for the API.

![api-lifecycle-diagram](/images/API-Lifecycle-complete.jpg)

### Technical Preview

We may release new APIs, features, and operations as a Technical Preview. This allows you to review upcoming capabilities and provide feedback. Additionally, it assists us in making sure we are providing the right solutions and expected functionality.

You may use APIs in Technical Preview for free while they are in preview. Do not use these APIs in Production. They are available for testing only, to gather feedback before releasing for General Availability.

**Note**: We reserve the right to remove items in Technical Preview from the ecosystem at any time. In which case, we will no longer support them.

### General Availability

APIs in General Availability are available for production ready use. We provide full support for these APIs. APIs can remain in General Availability for an unlimited period however, substantial changes to the structure and function of the API can require a change in version. In these cases, when we release the new API version to GA, we transition the older version to a Deprecated status and you are encouraged to move to the new version.

### Deprecated

We deprecate an API when we replace it by a different API or update it to a new version. If you are using the deprecated API for your solutions, you are encouraged to update to the new API to take advantage of the new capabilities. We provide limited support to the deprecated API however, we fully support upgrading to a new version during this time. This policy excludes new development on a deprecated API. New customers must use the currently released version.

We keep deprecated APIs available and supported for a maximum of one year.

### End Of Support

When an API is deprecated, we keep it available for one year, allowing time for you to upgrade. After this time, we consider it at End of Support and remove it from the iTwin Platform ecosystem.

## Support Services

| **Technical Preview** | **General Availability**         | **Deprecated**                             | **End Of Support**                |
| --------------------- | -------------------------------- | ------------------------------------------ | --------------------------------- |
| **Limited Support**   | **Full Support**                 | **Limited Support**                        | **Upgrade Only**                  |
| GitHub community      | Bentley support                  | Bentley support (for one year)             | Upgrade to the latest API version |
| Stack Overflow        | GitHub community                 | Github community                           |                                   |
| Security updates      | Stack Overflow                   | Security updates                           |                                   |
| New functionality     | Security updates                 | Maintenance updates (Bentley's discretion) |                                   |
| Bug fixes             | Maintenance updates              | No enhancements or new functionality       |                                   |
|                       | New functionality - Non breaking |                                            |                                   |
