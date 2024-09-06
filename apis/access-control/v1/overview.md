# Access Control API

The Access Control API provides a full encompassing suite of functionality to manage access on your digital twins. With this API, you can manage your digital twin's members and each member's permissions on the digital twin.

## Role-Based Access Control

The Access Control API is built following role-based access control (RBAC) principles, which is an approach to authorizing users. RBAC is defined around roles, permissions, and user role assignments. Permissions are the fundamental unit of approval to a resource. Roles are a grouping mechanism used to aggregate permissions, and are assigned to members of an iTwin. When a role is assigned to a user, the user is authorized to perform actions or access data based on those permissions.

## iTwin Permissions

iTwin access control is enforced by permissions. A permission grants access to an API function. In other words, all iTwin Platform APIs enforce the requirements of one or many permissions in order to call it's endpoints. The permissions required by an API endpoint are documented in the Authorization section of the API reference documentation.

## iTwin Roles

Roles are used to group permissions. Typically, the permissions grouped in a role are aligned with user personas and are assigned to those personas accordingly (e.g. iTwin Administrator). iTwin roles are defined on each iTwin and are scoped such that they must be assigned on that iTwin.

## iTwin Members

iTwin Members are the list of users which have been assigned a role on an iTwin. Each member has a list of permissions which have been assigned to them using roles, which permit them to perform actions on an iTwin.

### Service Applications

Service applications, used for machine-to-machine communication, may also be authorized to access resources for a given iTwin. Just like iTwin members, service applications have an identity. This allows you to authorize service applications using the same process as a normal iTwin member. The email for the application is found in the application registration portal. To authorize, a role must be assigned to the service application on an iTwin.
