---

Creates an ApiKey used to connect OData v4 compliant applications to [Data Access](/apis/insights-v2/operations/odata/) endpoints.

The generated `apiKey` can be used in the password field of `Basic` authentication in applications or scipts, or used directly in the `Authorization` header of a request: `Authorization: Basic {apiKey}`.

ApiKeys are valid for a maximum of 6 months and not extendable. ApiKeys must be rotated when they expire.

{!ApiKeyTryItOutLimitations.md!}

{!InsightsPermissions.md!}

{!RateLimits.md!}

---
