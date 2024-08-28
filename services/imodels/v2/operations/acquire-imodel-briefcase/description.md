---

Acquires a new [Briefcase](https://www.itwinjs.org/learning/glossary/#briefcase).

Briefcases are the local copies of iModel that users can acquire to work with the iModel. Users can make changes to their copy of iModel and then push them as a single Changeset file into iModelHub. For more information on Briefcases see [working with Briefcases](https://www.itwinjs.org/learning/imodelhub/briefcases/).

**Note:** The total number of Briefcases a single user can acquire is limited. The error code `ResourceQuotaExceeded` is returned when you exceed the limit. The current limit is 100 total briefcases.

The number of Briefcases a single user can acquire per minute is also limited. The error code `RateLimitExceeded` is returned when you exceed the limit. The current limit per minute is 100.

{!Authorization.md!}

{!iModelsPermissions.md!}

{!RateLimits.md!}

---
