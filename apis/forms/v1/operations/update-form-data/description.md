---

Modifies the provided properties of the specified form to match the values provided in the request.

Setting a property value to null in the request will set the corresponding property value to null on the form. However, omitting a property from the request body entirely will leave that property's current value on the form unchanged.  Also, setting an object (other than "properties") to null will have the same effect as setting each individual property in that object to null.

### Permissions

To use this endpoint, the user is required to have different Forms permission levels (for the iTwin, or for the form's definition if form definition security is specified) based on the changes being made:

- Change to the `status` property: **Approve** (`Forms_ApproveAccess`) permission
- Change to the `assignee` or `assignees` property: **Assign** (`Forms_AssignAccess`) or **Approve** permission
- Changes to other properties: **Create/Modify** (`Forms_CreateAccess`) permission

**Full Access** (`Forms_FullAccess`) will satisfy all of these requirements.

{!Authorization.md!}

---