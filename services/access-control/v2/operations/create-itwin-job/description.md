---

Create a new iTwin job. iTwin jobs allow you to preform actions on an iTwin in bulk.

Currently there are three types of supported actions:

- `assignRoles`
- `unassignRoles`
- `removeMembers`

Note: If the user being assigned roles in the `assignRoles` action is not a member of the iTwin, they will be added to the iTwin with the provided roles.

`assignRoles` and `unassignRoles` actions have a limit of 100 roles per group of actions. `removeMembers` has a limit of 100 emails.

{!Authorization.md!}

{!iTwinsRBACPermission.md!}

---
