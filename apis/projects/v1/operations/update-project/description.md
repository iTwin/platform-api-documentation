---

Update the specified project.

For updates, all properties are optional. The request payload only needs to contain the properties that you would like to update. 

{!ProjectsDeprecated.md!}

{!Authorization.md!}

### Authorization
If a user is affiliated with an Organization, then the user must be an Organization Administrator in order to update a project that is owned by the Organization.  
Example: john.doe@example.com is an Organization Administrator that works for Example Industries that has an account with Bentley. John will be able to update any project that belongs to Example Industries. 

An Organization Administrator must have at least one of the following roles assigned in User Management: Account Administrator, Co-Administrator, or CONNECT Services Administrator. For more information about User Management please visit our Bentley Communities [Licensing, Cloud, and Web Services](https://communities.bentley.com/communities/other_communities/licensing_cloud_and_web_services/w/wiki/50711/user-management-2-0) wiki page.

A user that is not affiliated with an Organization can update projects that are owned by the user account.  
Example: jane.doe@gmail.com is an independent contractor that does not have an account with Bentley. Jane will be able to update any project that belong to Jane. Jane owns any project that she created.

---
