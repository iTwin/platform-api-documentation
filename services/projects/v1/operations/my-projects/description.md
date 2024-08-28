---

Retrieves a list of projects that can be accessed by the logged in user. The user is determined by the authentication token. See the Authorization section for information on how access rights are determined.

{!ProjectsDeprecated.md!}

{!Authorization.md!}

### Authorization

User must be an Organization Administrator for the Organization that owns a given project or be a project team member.

An Organization Administrator must have at least one of the following roles assigned in User Management: Account Administrator, Co-Administrator, or CONNECT Services Administrator. For more information about User Management please visit our Bentley Communities [Licensing, Cloud, and Web Services](https://communities.bentley.com/communities/other_communities/licensing_cloud_and_web_services/w/wiki/50711/user-management-2-0) wiki page.

### Response

By default, each project in the returned list of projects will have only the project id, display name and project number.

A full representation of each project can be returned by specifying the *prefer* header that includes a value of *return=representation*.

---
