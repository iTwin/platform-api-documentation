---

Configures RBAC user permissions for the individual iModel. Specified permissions are assigned to the provided user. 

Individual iModel permissions allow to have more granular permissions than assigned at iTwin level. This either broadens or shrinks the set of permission the user has at iTwin level. That is, once at least one user permission is configured on the given iModel, then this configuration takes precedence over permissions configured at iTwin level.

Role and User permissions are mutually exclusive and cannot be configured for an iModel at the same time.

Please refer to [Access Control API](https://developer.bentley.com/apis/access-control-v2/overview/) to learn more about Role Based Access Control principles in general.

iModel permissions that could be assigned to the provided user:

`imodels_webview` - allows to view iModel in web browser, but does not allow to get its local copy and view in desktop app.

`imodels_read` - allows to open and view an iModel only in read-only state.

`imodels_write` - allows to make changes to an iModel. Allows to create and modify named versions. Allows to create mapping between PW connection and iModel to facilitate bridges.

`imodels_manage` - allows to manage locks, codes or local copies for the entire iModel.

{!Authorization.md!}

{!iModelsPermissions.md!}

{!RateLimits.md!}

---