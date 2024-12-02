Delete the specified webhook. Once deleted, your webhook will stop receiving events.

#### Authentication

The Webhooks API V2 can only be called by Service Applications. This request requires an `Authorization` header with a valid Bearer token with the `{scope}` scope. For more information on Service Applications and how to obtain an access token can be found [here](https://developer.bentley.com/tutorials/authorize-service/). A list of your Service Applications can be found [here](https://developer.bentley.com/my-apps).

#### Authorization

The Service Application must have the `webhooks_maintainer` permission assigned at the iTwin level or be an Organization Administrator for the Organization that owns a given iTwin.

An Organization Administrator must have at least one of the following roles assigned in User Management: Account Administrator, Co-Administrator, or CONNECT Services Administrator. For more information about User Management please visit our Bentley Communities [Licensing, Cloud, and Web Services](https://bentleysystems.service-now.com/community?id=kb_article_view&sys_kb_id=1e5410491b7d8a90f3fc5287624bcb57) wiki page.
