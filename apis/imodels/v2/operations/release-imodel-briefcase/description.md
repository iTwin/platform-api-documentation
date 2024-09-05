---

Deletes the specified [Briefcase](https://www.itwinjs.org/learning/glossary/#briefcase).

Briefcases are the local copies of iModel that users can acquire to work with the iModel. Users can make changes to their copy of iModel and then push them as a single Changeset file into iModelHub. For more information on Briefcases see [working with Briefcases](https://www.itwinjs.org/learning/imodelhub/briefcases/).

{!Authorization.md!}

### Authorization

To release any Briefcase user must have `imodels_manage` permission assigned at the iModel level. If permissions at the iModel level are not configured, then user must have `imodels_manage` permission assigned at the iTwin level. To release a Briefcase that the user owns `imodels_webview` permission is enough.

Alternatively the user should be an Organization Administrator for the Organization that owns a given iTwin the iModel belongs to.

For more information please refer to [Account Administrator](https://developer.bentley.com/apis/access-control-v2/overview/#accountadministrator) documentation section on Access Control API documentation page.

{!RateLimits.md!}

---