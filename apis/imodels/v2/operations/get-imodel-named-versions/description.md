---

Retrieves a list of Named Versions for the iModel specified by the iModel id.

Every [Changeset](https://www.itwinjs.org/learning/glossary/#changeset) on the timeline creates a new version of the iModel. However, some points on the timeline can represent important milestones or significant events to be saved. iModelHub provides a way to mark a point on the timeline with a name. These time points are referred to as Named Versions.

### Notes

The `Prefer` header can be used to specify how much result metadata is desired by the client. The `Prefer` request header field is used to indicate that particular server behaviors are preferred by the client but are not required for successful completion of the request.

This operation supports `"return=representation"` and `"return=minimal"` preferences.

The `"return=representation"` preference indicates that the client prefers that the server include an entity representing the current state of the resource in the response to a successful request.
The `"return=minimal"` preference indicates that the client wishes the server to return only a minimal response to a successful request. This is the default preference if `Prefer` header is not specified.

{!Authorization.md!}

{!iModelsPermissions.md!}

{!RateLimits.md!}

---
