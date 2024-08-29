---

Add new project team member

### Notes

The POST body MUST include either a *userId* property or an *e-mail* property.

When adding members by ids, the POST body MAY include the roleIds property, which MUST be defined as an array of role IDs that will be assigned to new team member.

When adding members by names, the POST body MAY include the roleNames property, which MUST be defined as an array of role names that will be assigned to new team member.

When adding members *Team Member* role will be assigned to all members. *Team Member* role grants member write access to Storage and Forms APIs. *Team Member* can be removed from any member if access to Storage and Forms APIs is not desired. 

{!ProjectsDeprecated.md!}

{!Authorization.md!}

{!RbacPermissions.md!}

---
