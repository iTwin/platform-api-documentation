# iTwins API

The iTwins API provides a full encompassing suite of functionality to manage your digital twins. With this API, you can create iTwins, control their lifecycle, discover repositories associated to them, query to get your recently used iTwins, and manage your favorite iTwins.

## iTwins

The iTwin is Bentley's digital twin object and the iTwins API is used to manage your iTwins. For non-technical information about managing your iTwins, please see [Digital Twin Management](https://developer.bentley.com/api-groups/data-management/) in the Twin Platform documentation.

A digital twin exists in many shapes and sizes, or in engineering terms, many disciplines and phases. iTwins have properties to help describe the digital twin's purpose, which aligns with its discipline and phase. Specifically, an iTwin's `class` and `subClass` fields are used to specify its classification (e.g. _Thing_ & _Asset_ are used to classify an _operating asset_ digital twin, while _Endeavor_ & _Project_ are used to classify a _capital project_ digital twin). Use the iTwin's `type` field to further refine the iTwin's purpose. The iTwin's `displayName` and `number` fields are typical engineering properties for projects and assets, and can be used as such; Each of these fields are required to be unique for each `subClass`. Finally, modify the `status` property, with possible values of _active_, _inactive_, and _trial_ to manage the lifecycle of the iTwin. The examples below show the use of these properties in engineering use-cases:

A digital twin of the US Route 202 highway

```json
{
  "id": "051b685f-4168-4e2d-900e-49d57e171513",
  "class": "Thing",
  "subClass": "Asset",
  "type": "Highway",
  "displayName": "US Route 202",
  "number": "HWYUSR202",
  "status": "active"
}
```

A digital twin of a project to widen the 61N section of the US Route 202 highway

```json
{
  "id": "01a5b73e-d5d3-47fc-ae3e-253365d93eb9",
  "class": "Endeavor",
  "subClass": "Project",
  "type": "Construction",
  "displayName": "US Route 202 Section 61N Expansion",
  "number": "HWYUSR202S61NEXP",
  "status": "active"
}
```

## iTwin Classes and SubClasses

All iTwins are comprised of the same set of attributes and capabilities.  Developers can use the class and subclass to group and categorize like-minded iTwins..  Below are the available set classes and subclasses for a developer to choose from along with a description to help aid in the determination of which subclass is appropriate for your use case.

- class: __Thing__ - Use this class when the iTwin being created references physical infrastructure or real-world entity.

    -	subClass: __Asset__ - Use this subclass when the iTwin being created references a property or piece of infrastructure.  Examples of an Asset include a building, bridge, or a piece of equipment that requires its own digital twin. 

    -	subClass: __Portfolio__ - Use this subclass when the iTwin being created references a collection of objects or a spatial region.  Please note that entities of these iTwins may be linked to other iTwins but are not required.  Examples of a Portfolio include a city, state, rail network, or the collection of properties owned by an organization.

- class: __Endeavor__ - Use this class when the iTwin being created references the process involved in the engineering, constructing, operating and maintaining of infrastructure.

    -	subClass: __Project__ - Use this subclass when the iTwin being created references work being done to produce a deliverable.  Examples of a Project include design, engineering or construction projects.

    -	subClass: __Program__ - Use this subclass when the iTwin being created references the coordination of several related efforts managed and delivered as a single package.  Please note, entities of these iTwins may be linked to other iTwins but are not required.  Examples of a Program include the development of a new rail network.

    -	subClass: __WorkPackage__ - Use this subclass when the iTwin being created references a group of related tasks within a project.  Examples of a WorkPackage include engineering and construction work packages or sub-projects to support the supply chain.

iTwins can be related to other iTwins using a parent-child relationship.  Some common or recommended relationship hierarchies are listed below..

<ul> 
<li>Portfolio
<ul> 
<li style="list-style-type: none;">Asset</li> 
<li style="list-style-type: none;">Program</li> 
<li style="list-style-type: none;">Project</li> 
</ul>
<li>Asset
<ul> 
<li style="list-style-type: none;">Program</li> 
<li style="list-style-type: none;">Project</li> 
</ul>
<li>Program
<ul> 
<li style="list-style-type: none;">Project</li> 
<li style="list-style-type: none;">WorkPackage</li> 
</ul>
<li>Project
<ul> 
<li style="list-style-type: none;">WorkPackage</li> 
</ul>
</ul>

## Account

There is a special iTwin SubClass named Account. An Account iTwin is created automatically for each organization and serves as the root of the hierarchy for all iTwins created by that organization.  The organization that owns the Account will also own all iTwins under the Account. 

<pre>    Account: Acme Corp.
          iTwin XYZ
          iTwin ABC
               iTwin AA
               iTwin BB
                    iTwin B1
                    iTwin B2
					
</pre>

There is an API for getting the Account of an iTwin no matter where it exists in the hierarchy. You could use this [API](https://developer.bentley.com/apis/itwins/operations/get-itwin-account/) to find out that iTwin B1 is owned by Acme Corp.  There is an iTwinAccountId property on every iTwin that allows you to query for iTwins owned by Acme Corp. This is useful since you could have access to iTwins in different organizations.
 
You could also have access to different Accounts. If Acme Corp acquires Soylent Corp, then Acme will now own two Accounts and the iTwins under both. As an employee of Acme Corp, my primary Account will be Acme Corp. Any iTwin that I create will be created in the Acme Corp Account unless specified otherwise. There are APIs for [getting all Accounts](https://developer.bentley.com/apis/itwins/operations/get-my-itwins/) that I can access or just [my primary Account](https://developer.bentley.com/apis/itwins/operations/get-my-primary-account/).
 
We occasionally get a request to move iTwins from one Account to another. iTwin users may not notice but it is important for developers to realize that while the iTwinAccountId is not updateable, it can change via a help request.

## Account Roles

Organization administrators can use the [Access Control API](https://developer.bentley.com/apis/access-control/) to define roles for their Account. The Roles defined for an Account can then be used by any iTwin in the hierarchy under the Account. This makes it convenient for administrators to define and manage common roles in one place. Administrators for individual iTwins can define additional roles specific to their iTwin.

## iTwin Access Control

Each and every iTwin implicitly contains built-in access control, managed using the [Access Control API](https://developer.bentley.com/apis/access-control/). The Access Control API follows Role Based Access Control security principles, which provides the capability to group permissions into roles and assign those roles to users on an iTwin. An iTwin role assignment gives you permissions on that iTwin and enables that functionality permitted by the permission. These permissions are required by many iTwin Platform services and you will see specific permission requirements documented in each service endpoint's Authorization section.

Access Control on iTwins gives you the capability to organize your iTwin's members working on your digital twins, which by way of the iTwin properties, is also aligned with the iTwin's purpose. Using different role assignments for different member personas allows you to manage your member's access control accordingly. Likewise, the [Access Control API](https://developer.bentley.com/apis/access-control/) allows for external member invitations -- if someone outside of your organization is collaborating on your iTwin, simply invite them to your iTwin via a role assignment.

## iTwin Repositories

Digital twins are all about the data, whether that be engineering modeling data, IoT sensor data, drone footage, 3d mesh drawings, or files and folders. The discovery of that data can be cumbersome and requires previous knowledge of the available data repositories. Thus, the iTwins Repository API provides a way to discover which data repositories contain data for your iTwin.

Additionally, there are many external data repositories used for digital twins. Use the repository endpoints in the iTwins API to associate these external repositories to your digital twin.

## Client Packages

Open source Typescript client packages are available for the iTwins API:

- @itwin/itwins-client - [NPM registry](https://www.npmjs.com/package/@itwin/itwins-client)
