---

Add new iTwin owner members. iTwin Owners are users which have full control over the iTwin. Each owner is granted all permissions on the iTwin, allowing them to perform any action on the iTwin they own.

Users which are external (i.e. not in the same organization as the iTwin) are not automatically added to the iTwin. Instead, they're invited. Users which are not external, are immediately added as members on the iTwin.

Invited individuals will recieve an invitation via Email, where they'll be prompted to accept the invitation. Upon accepting, they'll then become a member of the iTwin.

### Authentication

Requires `Authorization` header with valid Bearer token for scope `itwin-platform`.

For more documentation on authorization and how to get access token visit [OAUTH2 Authorization](https://developer.bentley.com/apis/overview/authorization/) page.

You must be an owner to add other owners.

### Authorization

User must have the `administration_invite_member` permission assigned at the iTwin level or be an Organization Administrator for the Organization that owns a given iTwin.

An Organization Administrator must have at least one of the following roles assigned in User Management: Account Administrator, Co-Administrator, or CONNECT Services Administrator. For more information about User Management please visit our Bentley Communities [Licensing, Cloud, and Web Services](https://bentleysystems.service-now.com/community?id=kb_article_view&sys_kb_id=1e5410491b7d8a90f3fc5287624bcb57) wiki page.

---
