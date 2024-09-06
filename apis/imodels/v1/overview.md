# iModels API

The iModels API provides the ability to access and manage information about iModels. An iModel is a specialized information container for exchanging data associated with the lifecycle of infrastructure assets. iModels were created to facilitate the sharing and distribution of information regardless of the source and format of the information. Project teams use iModels to ensure that information flows easily, completely, and accurately between and within design, construction, and operations environments. iModels are self-describing, geometrically precise, open, portable, and secure. iModels encapsulate component information, business properties, geometry, graphics, and relationships in a format that is open, providing standard interfaces for applications from multiple vendors.

## iModelHub service

Under iModels API is iModelHub cloud service that enables alignment, accountability and accessibility of infrastructure digital twins. It is the control center for iModels and is responsible for coordinating concurrent access to iModels as well as changes made to them in a form of Changesets. Its main role is to maintain the sequence of Changesets that forms an iModel's timeline. Like an accounting system does for financial transactions, iModelHub holds a ledger of all changes to an iModel. With iModelHub you no longer need to question what might have changed. It stores and manages the record of who did what and when. iModelHub stores the change itself rather than just the result of the change.

### Changesets

A Changeset represents a group of changes to an iModel. Changesets are created whenever a local copy of the iModel is modified and reflect the union of all additions, deletions, and modifications over a period of time. Changesets are assigned an identifier when they are uploaded to iModelHub and every Changeset stores the identifier of its parent Changeset. In this way the chain of Changesets for an iModel in iModelHub forms its "timeline of changes".

### Named versions

Every Changeset on the timeline creates a new version of the iModel. However, some points on the timeline can represent important milestones or significant events to be saved (for example, for a design review). A Named Version can be used to mark a point on the timeline with a name. Named versions are cached to make them faster to access.

## Samples

For more information on how to use the API, please check the [iModels API Management Workflows Sample Application on github](https://github.com/iTwin/imodels-api-management-workflow-sample-app).

## Client Packages

Open source TypeScript client packages are available for iModels API:
- @itwin/imodels-client-management - [NPM registry](https://www.npmjs.com/package/@itwin/imodels-client-management), [documentation](https://github.com/iTwin/imodels-clients/blob/main/docs/IModelsClientManagement.md)
- @itwin/imodels-client-authoring - [NPM registry](https://www.npmjs.com/package/@itwin/imodels-client-authoring), [documentation](https://github.com/iTwin/imodels-clients/blob/main/docs/IModelsClientAuthoring.md)

Please check the [general documentation](https://github.com/iTwin/imodels-clients/tree/main/docs) for explanation on the difference between the packages.