<!-- Copyright (c) Bentley Systems, Incorporated. All rights reserved.            -->
<!-- See LICENSE in the project root for license terms and full copyright notice. -->

# API Versioning and Release Lifecycle

## API Versions

All APIs are versioned and the version number is embedded in the **Accept** header as shown below.

```HTTP
GET https://api.bentley.com/users/me HTTP/1.1
Authorization: Bearer JWT_TOKEN
Accept: application/vnd.bentley.itwin-platform.v1+json

```

We are continually improving our APIs. The API version number will be incremented when we introduce a breaking change. A breaking change is a non-backward compatible change in the API that can cause applications using the API to no longer function as expected. The following are examples of changes that are not backward compatible:

- Changing the URI of the resource
- Changing the method used to access a resource
- Adding new required request parameters
- Changing a field name or deleting a field from the response

The following changes are backward compatible:

- Adding new API endpoints
- Adding new optional request parameters
- Adding new fields to the response

As much as possible, we will provide notice of a breaking change well before its release. When the new version of an API is released, we provide one year for you to update your applications. The exact amount of notice we provide may vary depending on why the breaking change is necessary.

## API Release Status

API product releases have a well-defined lifecycle. The release status determines the level of support offered for the API.

![api-lifecycle-diagram](/images/API-Lifecycle-complete.jpg)

### Technical Preview

New APIs, new features, and new operations may be released as a technical preview. This allows you to review upcoming capabilities and provide feedback. Additionally, it assists our team in making sure we are providing the right solution and the functionality works as it should.

APIs in Tech Preview are free to use during the time they are in preview. These APIs should not be used in Production. They are available for testing to gather feedback before releasing for General Availability.

**Note**: Items in Tech Preview can be removed from the ecosystem at any time. In which case, they will no longer supported.

### General Availability

APIs in general availability are available for production and ready to use. Full support is provided. APIs may remain in General Availability for an unlimited period however, substantial changes to the structure and function of the API will require a change in version. In these cases, when the new version reaches GA, the older version will be moved to a Deprecated status and you are encouraged to move to the new version.

### Deprecated

An API is deprecated when it has been replaced by a different API or updated to a new version. If you are using the API for your solutions, you are encouraged to update to the new API to take advantage of the new capabilities. Limited support is given on the deprecated API however, upgrading to a new version is fully supported during this time. This does not include new development on a deprecated API. New customers must develop on the currently released version.

Deprecated APIs will remain available and will be supported for a maximum of one year.

### End Of Support

When an API is deprecated, it remains available for one year, allowing time for you to upgrade. After this time, it is considered at End of Support and will be removed from the iTwin Platform ecosystem.

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

<!-- ## Deprecation Guidelines

As with any software, APIs evolve to provide enhanced capabilities and a better experience for our developers and community. The result of this evolution is that APIs and components may change or be removed. While we strive to avoid breaking changes, there are cases where this is unavoidable. Our team uses the following guidelines to ensure you have the latest information and can adjust accordingly.

**What constitutes a breaking change or a deprecation plan?**

Breaking changes result in a deprecation plan for the affected API. The following descriptions explain what results in a breaking change.

**Breaking Change** – A breaking change is a non-backward compatible change in the API that can cause applications using the API to no longer function as expected. This may include a substantive change to the API, such as a function formatting change, or removing a property from an existing response. Adding new properties or operations in a forward-compatible way does not result in a breaking change. For example, adding a new endpoint or properties to an existing operation.

**Deprecation** – The deprecation of an API occurs when a breaking change has been introduced. An API released with a breaking change is released as a new version resulting in the previous version being deprecated. Additionally, if an API is being removed from the ecosystem, either from non-use or for some other reason, it will include a deprecation plan. In the case of the non-use of an API, the API may be deprecated immediately.

**How are deprecation plans communicated?**

As much as possible, we will provide notice of a breaking change well before its release. When the new version of an API is released, we provide one year for you to update your applications. The exact amount of notice we provide may vary depending on why the breaking change is necessary. The table below provides insight into our current versions, and if deprecation plans are in place, the anticipated date of deprecation.

[insert Support Timeline tables, future]
