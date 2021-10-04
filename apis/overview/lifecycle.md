<!-- Copyright (c) Bentley Systems, Incorporated. All rights reserved.            -->
<!-- See LICENSE in the project root for license terms and full copyright notice. -->

# API release lifecycle

## API versions

All APIs are versioned and the version number is embedded in the **Accept** header. Sample request:

``` HTTP
GET https://api.bentley.com/users/me HTTP/1.1
Authorization: Bearer JWT_TOKEN
Accept: application/vnd.bentley.itwin-platform.v1+json

```

We are continually improving our APIs. The API version number will be incremented when we introduce a breaking change that is not backwards compatible. The following are examples of changes that are not backward compatible:

- Changing the URI of the resource
- Changing the method used to access a resource
- Adding new required request parameters
- Changing a field name or deleting a field from the response

The following changes are backward compatible:

- Adding new API endpoints
- Adding new optional request parameters
- Adding new fields to the response

## API release status

API product releases have a well-defined lifecycle. The release status determines the level of support as described below.

| API release status   | Description                                                                                                                                                                                                                                                                                                                                              | Support              |
| -------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------- |
| Technology Preview   | New functionality is sometimes released early as a technology preview or beta version. Technology Previews are for evaluation only and are not intended for production work.                                                                                                                                                                             | Limited Support      |
| General Availability | An active commercial release for production work.                                                                                                                                                                                                                                                                                                        | Full Support         |
| Deprecated           | When a new API version has been released the previous version will be deprecated. Deprecated API versions will remain active in production for six months and developers should move to the new API version during that time period. New applications cannot use deprecated APIs. After six months a deprecated API version will move to End of Support. | Limited Support      |
| End of Support       | An API version that has been decommissioned and is no longer available in production.                                                                                                                                                                                                                                                                    | Support Discontinued |

## Support services

### Full Support

- Bentley technical support
- Community support
- Regular maintenance updates
- Regular enhancements with new functionality
- Security updates

### Limited Support

- Community support
- Maintenance updates at Bentley's discretion
- No enhancements or new functionality

### Support Discontinued

- Upgrade to the latest API version
