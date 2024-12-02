---

Retrieves a list of team members and their roles assigned to a specified project.

{!ProjectsDeprecated.md!}

{!Authorization.md!}

### Authorization

User must be an Organization Administrator for the Organization that owns a given project or be a project team member.

{!OrganizationAdministrator.md!}

### Response

By default, each member in the returned list of members will only have names of the roles that are assigned to the user.

A full representation of roles assigned to the member can be returned by specifying the *prefer* header that includes a value of *return=representation*.


---