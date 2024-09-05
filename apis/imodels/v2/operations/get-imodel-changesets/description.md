---

Retrieves a list of [Changesets](https://www.itwinjs.org/learning/glossary/#changeset) for the iModel specified by the iModel id.

[Changesets](https://www.itwinjs.org/learning/glossary/#changeset) form a linear timeline of the iModel changes. 
For more information on creating and retrieving Changesets using iTwin.js see [working with Changesets](https://www.itwinjs.org/learning/imodelhub/briefcases/).

### Notes

The `Prefer` header can be used to specify how much result metadata is desired by the client. The `Prefer` request header field is used to indicate that particular server behaviors are preferred by the client but are not required for successful completion of the request.

This operation supports `"return=representation"` and `"return=minimal"` preferences.

The `"return=representation"` preference indicates that the client prefers that the server include an entity representing the current state of the resource in the response to a successful request.
The `"return=minimal"` preference indicates that the client wishes the server to return only a minimal response to a successful request. This is the default preference if `Prefer` header is not specified.

{!Authorization.md!}

{!iModelsPermissions.md!}

**Note:** `download` property requires user to have at least `imodels_read` permission. If user has only `imodels_webview` permission `download` will always be null.

{!RateLimits.md!}

---
