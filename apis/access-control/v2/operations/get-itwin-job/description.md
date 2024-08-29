---

Retrieves the specified iTwin job for the specified iTwin.

By default this operation will only return the `status` of the iTwin job. To find the specific errors of the iTwin job, include `return=representation` in the `Prefer` header.

### Status

- `Active`: iTwin job is stil in progress.
- `Completed`: iTwin job completed without error.
- `PartialCompleted`: iTwin job completed with some actions failing. To find the specific errors of the iTwin job, include `return=representation` in the `Prefer` header.
- `Failed`: iTwin job completed with all actions failing. To find the specific errors of the iTwin job, include `return=representation` in the `Prefer` header.

### Authentication

Requires `Authorization` header with valid Bearer token for scope `itwin-platform`.

For more documentation on authorization and how to get access token visit [OAUTH2 Authorization](https://developer.bentley.com/apis/overview/authorization/) page.

### Authorization

User must have the `{permission}` permission assigned at the iTwin level or be an Organization Administrator for the Organization that owns a given iTwin.

An Organization Administrator must have at least one of the following roles assigned in User Management: Account Administrator, Co-Administrator, or CONNECT Services Administrator. For more information about User Management please visit our Bentley Communities [Licensing, Cloud, and Web Services](https://bentleysystems.service-now.com/community?id=kb_article_view&sys_kb_id=1e5410491b7d8a90f3fc5287624bcb57) wiki page.

---
