---

Updates existing component in user's organization context.

### Notes

To update a component request body must contain all the properties desired for the component since this will replace existing component with current component definition. DisplayName and status are required properties.

Component status values are:
-Draft
-Published 
-Checked
-Approved
-Archived

### Associated Entities
A component can have associated entities, e.g catalogs, application, category, manufacturer. These values should be valid Ids of existing entities.

{!Authorization.md!}

{!LibraryPermissions.md!}

{!RateLimits.md!}

---