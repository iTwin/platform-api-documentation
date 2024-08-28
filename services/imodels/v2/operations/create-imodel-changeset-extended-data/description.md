---

Adds application specific data to the specified [Changeset](https://www.itwinjs.org/learning/glossary/#changeset).

Extended data is an application specific data associated to the Changeset. This data is not interpreted by the service. Extended data must be a valid json object encoded as base64 string.

Extended data can only be set once by the principal who created the Changeset. Maximum supported data field size is 204800 bytes (200 KiB).

{!Authorization.md!}

{!iModelsPermissions.md!}

{!RateLimits.md!}

---