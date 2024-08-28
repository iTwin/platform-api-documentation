---

Retrieves a list of [reality data](https://www.itwinjs.org/learning/glossary/#realitydata) instances belonging to the specified iTwin.

The retrieved instances are those for which you have the required access rights, relative to the specified iTwin. 

The `iTwinId` is optional. If you don't provide it, the retrieved [reality data](https://www.itwinjs.org/learning/glossary/#realitydata) instances will be relative to general access rights provided by your organization. These rights are usually more restrictive, so we recommend using the `iTwinId` parameter for exhaustive results.

### Notes

The `Prefer` header can be used to specify how much result metadata is desired by the client. The `Prefer` request header field is used to indicate that particular server behaviors are preferred by the client but are not required for successful completion of the request.

This operation supports `"return=representation"` and `"return=minimal"` preferences.

The `"return=representation"` preference indicates that the client prefers that the server include an entity representing the current state of the resource in the response to a successful request, i.e., all properties are included in the response.
The `"return=minimal"` preference indicates that the client wishes the server to return only a minimal response to a successful request. This is the default preference if `Prefer` header is not specified.

{!Authorization.md!}

### Authorization

User must be an Organization Administrator for the Organization that owns a given iTwin or must have access to context.

An Organization Administrator must have at least one of the following roles assigned in User Management: Account Administrator, Co-Administrator, or CONNECT Services Administrator. For more information about User Management please visit our Bentley Communities Licensing, Cloud, and Web Services wiki page.

{!RateLimits.md!}

---