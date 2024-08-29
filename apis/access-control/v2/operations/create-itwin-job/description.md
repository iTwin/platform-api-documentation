---

Create a new iTwin job. iTwin jobs allow you to preform actions on an iTwin in bulk.

Currently there are three types of supported actions:

- `assignRoles`
- `unassignRoles`
- `removeMembers`

Note: If the user being assigned roles in the `assignRoles` action is not a member of the iTwin, they will be added to the iTwin with the provided roles.

`assignRoles` and `unassignRoles` actions have a limit of 100 roles per group of actions. `removeMembers` has a limit of 100 emails.

### Authentication

Requires `Authorization` header with valid Bearer token for scope `itwin-platform`.

For more documentation on authorization and how to get access token visit [OAUTH2 Authorization](https://developer.bentley.com/apis/overview/authorization/) page.

### Authorization

User must have the `{permission}` permission assigned at the iTwin level or be an Organization Administrator for the Organization that owns a given iTwin.

An Organization Administrator must have at least one of the following roles assigned in User Management: Account Administrator, Co-Administrator, or CONNECT Services Administrator. For more information about User Management please visit our Bentley Communities [Licensing, Cloud, and Web Services](https://bentleysystems.service-now.com/community?id=kb_article_view&sys_kb_id=1e5410491b7d8a90f3fc5287624bcb57) wiki page.

---
