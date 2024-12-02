---

Retrieves a list of [Briefcases](https://www.itwinjs.org/learning/glossary/#briefcase) for the iModel specified by the iModel id.

Briefcases are the local copies of iModel that users can acquire to work with the iModel. Users can make changes to their copy of iModel and then push them as a single Changeset file into iModelHub. For more information on Briefcases see [working with Briefcases](https://www.itwinjs.org/learning/imodelhub/briefcases/).

### Notes

The `Prefer` header can be used to specify how much result metadata is desired by the client. The `Prefer` request header field is used to indicate that particular server behaviors are preferred by the client but are not required for successful completion of the request.

This operation supports `"return=representation"` and `"return=minimal"` preferences.

The `"return=representation"` preference indicates that the client prefers that the server include an entity representing the current state of the resource in the response to a successful request.
The `"return=minimal"` preference indicates that the client wishes the server to return only a minimal response to a successful request. This is the default preference if `Prefer` header is not specified.

{!Authorization.md!}

{!iModelsPermissions.md!}

{!RateLimits.md!}

---
