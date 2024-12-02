---

Retrieves a list of permissions the user has for the specified iModel. iModels permissions may be configured on an iTwin level or an iModel level. iModel level permissions can be configured [per role](https://developer.bentley.com/apis/imodels-v2/operations/update-imodel-role-permissions/) or [per user](https://developer.bentley.com/apis/imodels-v2/operations/update-imodel-user-permissions/). This operation will return permissions configured for this specific iModel or iTwin permissions if iModel permissions are not configured.

`imodels_webview` - allows to view iModel in web browser, but does not allow to get its local copy and view in desktop app.

`imodels_read` - allows to open and view an iModel only in read-only state.

`imodels_write` - allows to make changes to an iModel. Allows to create and modify named versions. Allows to create mapping between PW connection and iModel to facilitate bridges.

`imodels_manage` - allows to create an iModel. Allows to configure access per iModel. Allows to manage locks, codes or local copies for the entire iModel. This permission is both iModel and iTwin level permission, but Create iModel operation requires that user has `imodels_manage` permission on the iTwin level.

`imodels_delete` - allows to delete an iModel. This permission is only available on the iTwin level.

{!Authorization.md!}

{!iModelsPermissions.md!}

{!RateLimits.md!}

---