---

Retrieves the specified iTwin job for the specified iTwin.

By default this operation will only return the `status` of the iTwin job. To find the specific errors of the iTwin job, include `return=representation` in the `Prefer` header.

### Status

- `Active`: iTwin job is stil in progress.
- `Completed`: iTwin job completed without error.
- `PartialCompleted`: iTwin job completed with some actions failing. To find the specific errors of the iTwin job, include `return=representation` in the `Prefer` header.
- `Failed`: iTwin job completed with all actions failing. To find the specific errors of the iTwin job, include `return=representation` in the `Prefer` header.

{!Authorization.md!}

{!iTwinsRBACPermission.md!}

---
