---

Creates a [reality data](https://www.itwinjs.org/learning/glossary/#realitydata).

As shown in the request section below, you must provide a request body.

You MUST provide the `displayName` and `type` properties.

The `rootDocument` property is not required but highly recommended. It is the entry point for consuming applications to read the content of the Reality Data. [See RootDocument property](https://developer.bentley.com/apis/reality-management/rm-rd-details/#root-document)

For more details on each property, see [Reality Data Properties](https://developer.bentley.com/apis/reality-management/rm-rd-details/) in documentation.

After creation, the reality data will be associated to the specified iTwin.

{!Authorization.md!}

{!iTwinsRBACPermission.md!}

{!RateLimits.md!}

---