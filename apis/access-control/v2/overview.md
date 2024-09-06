# Access Control API [Github]

The Access Control API is a crucial part of administering your iTwins. It enables you to control access to iTwin Platform services on an iTwin, utilizing Role-Based Access Control (RBAC) principles. This documentation introduces Role-Based Access Control and explains how RBAC is applied to manage access to iTwin Platform services, on your iTwins.

## Role-Based Access Control

The Access Control API is built on three primary RBAC entities.

- **Permissions:** Unlocks capabilities available in an iTwin Platform service.
- **Roles:** Aggregates permissions and are assigned to members.
- **Members:** Individual users or a group of users which are assigned roles.

### Permissions

Permissions serve as the cornerstone of the API and determine what specific actions a user can perform. For instance, permissions are used in the iModels API to control who can create an iModel, in the iTwins API to regulate who can update iTwins, and in the Synchronization API to restrict the configuration and execution of iModel syncs.

The _Authorization_ section in the documentation for each API endpoint outlines the permissions needed for that API.

<img src="/images/ac-itwin-authorization-section-example.png" width="100%" height="auto" style="
    display: block;
    margin: auto;
    box-shadow: 0px 3px 15px rgba(0,0,0,0.2);"
    />

### Roles

Roles enable you to organize permissions and are assigned to one or more members. While not required, roles usually reflect the functional job duties within an organization and may be determined by various factors such as tasks or business operations.

<img src="/images/ac-role-grouping-example.jpg" width="50%" height="auto" style="
    display: block;
    margin: auto;"
    />

### Members

Members are users or groups which have been assigned a role, in turn giving them a set of permissions. Members may be individual users or groups of users as defined by Access Control Groups. See [Access Control Groups](#accesscontrolgroups) below for more information on managing groups of users. Members can be assigned more than one role. Likewise, the same role can be assigned to more than one member.

<img src="/images/ac-member-role-assignment-example.jpg" width="30%" height="auto" style="
    display: block;
    margin: auto;"
    />

## Managing access on an iTwin

The prior section outlines the general concepts of RBAC. It's important to note that role assignments only hold significance on a per iTwin basis. iTwins are considered atomic units and consist of data and members who work together within the iTwin. The permissions granted to a member on one iTwin do not transfer to other iTwins. For example, a member may be an Administrator in one iTwin and a participant in another.

The Access Control API enforces iTwin permission isolation by allowing configuration of how roles are defined and assigned. Roles that are defined on an iTwin, can only be assigned on that iTwin. Likewise, the permission definition of a role is isolated on the iTwin in which its defined. The example below highlights this concept; Notice that the role definitions and their assignments vary on the two iTwins. **Note:** The only exception to that rule is _Account Roles_. See the [Managing access using the Account iTwin](#managingaccessusingtheaccountitwin) section for more information.

<img src="/images/ac-itwin-configuration-example.jpg" width="90%" height="auto" style="
    display: block;
    margin: auto;"
    />

### Member Invitations

When adding a member, the member is either immediately assigned a role on the iTwin, or invited. Invitations are sent to the user which was invited, where they must accept the invitation before they become a member on the iTwin. Users which are "external" (users not in the same organization as the iTwin), are invited to iTwins, where "internal" users (users in the same organization as the iTwin) immediately become members.

### Managing access using the Account iTwin

_Note: For detailed information about the Account iTwin, refer to the [iTwins API documentation](/apis/itwins/#account)._

The Account iTwin offers robust capabilities. With the Account iTwin, roles and groups are defined in a centralized manner for the entire account and can be assigned on any iTwin owned by account. This ensures consistency in access control across iTwins and makes it easier to manage common personas and groups of individuals across multiple iTwins.

<img src="/images/ac-itwin-account-configuration-example.jpg" width="80%" height="auto" style="
    display: block;
    margin: auto;"
    />

In this example above, the Account iTwin has two role definitions and one group definition. These account-level roles and group are utilized in role assignments on the Asset and Project iTwin. Because the definition of the group and role is separate from the Asset and Project iTwin, their composition can be altered, and the changes will be reflected on the iTwins where they are assigned.

For example, if you want to add a new member to the Administrator Group, you can do so by updating the group definition on the Account iTwin, which will automatically add the new member as an administrator on all iTwins where the group is assigned the Admin Role. Similarly, if you want to modify the permissions of the Admin Role, you can do so by changing the role definition on the Account iTwin, which will automatically adjust the privileges of Administrators on every iTwin where the role is assigned.

### Account Administrator

The Bentley User Management application is used to determine the administrators of an Account iTwin. You must be assigned one of the following User Management roles to be defined as an Account Administrator in the iTwin Platform: Account Administrator, Co-Administrator, or CONNECT Services Administrator. To learn more about User Management, visit the Bentley Communities [Licensing, Cloud, and Web Services](https://bentleysystems.service-now.com/community?id=kb_article_view&sys_kb_id=1e5410491b7d8a90f3fc5287624bcb57) wiki page.

The Account Administrator has complete control and permissions on all iTwins in their account, without the need for a role assignment. This person can take any action on any iTwin within their account. As this is the highest authorization level available, use it judiciously and sparingly.

### iTwin Owner

As with an Account Administrator, the owner of an iTwin has full control and authorization over any iTwin in which they are designated as an owner. As the owner of an iTwin, you do not need a specific role assignment to work with that iTwin. The creator of the iTwin is designated as the owner by default and can manage the ownership list by adding or removing owners using the `/members/owners` API endpoints.

## Access Control Groups

Access Control groups provide the ability to manage groups of users at one time. As explained above, you can create groups on the Account iTwin to manage access across iTwins or create a group for an individual iTwin. Groups created on an individual iTwin are available only on that iTwin.

Groups can contain individual users. Groups can also reference Bentley Identity Management System (IMS) groups. By referencing an IMS group, you can manage groups of individuals in your Active Directory, while providing them access to iTwin Platform using role assignments.

<img src="/images/ac-groups-example.jpg" width="40%" height="auto" style="
    display: block;
    margin: auto;"
    />

## Client Packages

Open-source Typescript client packages are available for the Access Control API:

- @itwin/access-control-client - [NPM registry](https://www.npmjs.com/package/@itwin/access-control-client)

<div style="display: block; margin: auto; text-align: center;"><em>Note: Avatar images provided by pikisuperstar on Freepik</em></div>
