Creates a new webhook. On creation, webhook are inactive by default. To start receiving event, make a request to the [update webhook endpoint](/apis/webhooks-v2/operations/update-webhook/) with the `active` property set to `true`.

#### Callback Url (Required)

The URL of the public endpoint all events will be sent to. `HTTPS` is required for this URL. This endpoint will receive requests containing events that have been triggered by different actions throughout the iTwin Platform. A POST request will be sent to this url when an event is triggered with event details in the body of the POST request.

#### Scope (Required)

The `scope` property is required. Currently, there are two accepted value for `scope`: `Account`, `iTwin`.

All webhooks that are created with the `Account` scope are scoped to the account of the Service Application that created it. This means all events types the webhooks is subscribed to that happen inside that account will be sent to the webhook. Please be aware that Service Application's accounts are separate from the user's account that created the Service Application.

If the webhoook is created with the `iTwin` scope, then the property `scopeId` is required. `iTwin` scoped Webhooks will receive events for anything that is created directly inside of that `iTwin`.

#### Secret (Optional)

The `secret` property is optional. If no secret is provided in the request a secret is generated and sent back in the response. If provided, the secret must be at least 32 characters.

Before forwarding an event to the client, the webhook secret is used together with the whole request body to generate a `HMAC-SHA256` signature which is included in the `Signature` request header. Before doing anything with the received event the callback endpoint should handle the authorization process by using its own webhook secret copy together with request body and generate another signature on their end to validate the event source. If both signatures are the same, the event should be accepted as authorized. If the signatures do not match the event should be ignored. An example of this workflow can be found in our [tutorial](/tutorials/create-and-react-to-events-using-webhooks-v2/#23-add-event-authorization) or in our [samples](/apis/webhooks-v2/samples/).

#### Event Types (Required)

A list of events the webhooks will be subscribed to. See the [Events](/apis/webhooks-v2/available-events) page for a detailed list of all available event types.

#### Authentication

Webhooks can only be created by a Service Application. This request requires an `Authorization` header with a valid Bearer token with the `{scope}` scope. For more information on Service Applications and how to obtain an access token can be found [here](https://developer.bentley.com/tutorials/authorize-service/). A list of your Service Applications can be found [here](https://developer.bentley.com/my-apps).

#### Authorization

The Service Application must have the `webhooks_maintainer` permission assigned at the iTwin level or be an Organization Administrator for the Organization that owns a given iTwin.

An Organization Administrator must have at least one of the following roles assigned in User Management: Account Administrator, Co-Administrator, or CONNECT Services Administrator. For more information about User Management please visit our Bentley Communities [Licensing, Cloud, and Web Services](https://bentleysystems.service-now.com/community?id=kb_article_view&sys_kb_id=1e5410491b7d8a90f3fc5287624bcb57) wiki page.
