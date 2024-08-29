---

Create a new iTwin group.

### Authentication

Requires `Authorization` header with valid Bearer token for scope `itwin-platform`.

For more documentation on authorization and how to get access token visit [OAUTH2 Authorization](https://developer.bentley.com/apis/overview/authorization/) page.

### Authorization

A user can create a Group by being assigned the `administration_manage_groups` on the iTwin level. A user also can create a Group on an iTwin by either being an Organization Administrator for the Organization that owns the given iTwin, or an owner of the iTwin.

For creation of Groups on the Account iTwin, the user must be an Organization Administrator for the Organization.

An Organization Administrator must have at least one of the following roles assigned in User Management: Account Administrator, Co-Administrator, or CONNECT Services Administrator. For more information about User Management please visit our Bentley Communities [Licensing, Cloud, and Web Services](https://communities.bentley.com/communities/other_communities/licensing_cloud_and_web_services/w/wiki/50711/user-management-2-0) wiki page.

---
