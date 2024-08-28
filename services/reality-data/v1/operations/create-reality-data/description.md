---

Creates a [reality data](https://www.itwinjs.org/learning/glossary/#realitydata).

As shown in the request section below, you must provide a request body. 

You MUST provide the `displayName`, `classification` and `type` properties. 

Valid values for the `classification` property are: `Terrain`, `Imagery`, `Pinned`, `Model`, `Undefined`. For more details on each value, see [Reality Data Properties](https://developer.bentley.com/apis/reality-data/rd-details/) in documentation.

We recommend specifying a `projectId` in the request body, as it is used to choose the data center where the reality data is stored (the same as the project). If no `projectId` can be provided, the default data center of the organization is selected.

After creation, the reality data will be associated to the specified project.

{!Authorization.md!}

{!RbacPermissions.md!}

{!RateLimits.md!}

---