---

Creates component in user's organization context.

### Notes

To create a component, displayName and status are required properties.

Component status values are:
-Draft
-Published 
-Checked
-Approved
-Archived
By default a component is created with Draft state, subsequently it can be updated to other states during component's validation cycle. Only published components can be used in project scope.

### Associated Entities
A component can have associated entities, e.g catalogs, application, category, manufacturer. These values should be valid Ids of existing entities.

{!Authorization.md!}

{!LibraryPermissions.md!}

{!RateLimits.md!}

---