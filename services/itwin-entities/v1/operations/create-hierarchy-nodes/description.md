---

Create a new HierarchyNode for an entity. If a guid for the NodeId is not provided, a new GUID for nodeId will be assigned for each entity. Do not specify a parentId to create a root level node. The children list can be populated for any child nodes to be created under this HierarchyNode at the same time. A new nodeId can optionally be autamtically generated for the child nodes if the NodeId is not provided. The parentId for the child nodes also does not need to be specified and will be automatically populated. The children list can be a resursive, multi-level list.

{!Authorization.md!}

{!RbacPermissions.md!}

---
