# Reality Management API

Reality capture is the process of capturing the physical reality of an infrastructure asset, creating a representation of it, and maintaining it through continuous surveys. Reality models add real-world digital context to infrastructure iTwins. The Reality Management API provides the ability to retrieve information about the reality data that is associated with an infrastructure iTwin.

## Reality Data

Reality data properties represents the descriptive data related to a reality data. In addition to this, reality data content is stored as files and folders within a blob container uniquely associated to this reality data. Individual files and folders follow, from the root of the reality data, a normal file tree structure.

See the [Reality Data Properties](/apis/reality-management/rm-rd-details/) page for more detailed documentation.

## iTwins

Reality data are bound to iTwins. iTwins are used to represent engineering projects for an infrastructure asset. iModels, reality data, and engineering documents can be associated with a iTwin. The iTwins API is used to manage iTwins, iTwin team members, and iTwin roles. See more information in the [iTwins API Overview](/apis/itwins/overview/).

## Client Packages

Open source TypeScript client packages are available for the Reality Management API:

- @itwin/reality-data-client - [NPM registry](https://www.npmjs.com/package/@itwin/reality-data-client), [documentation](https://github.com/iTwin/reality-capture/tree/main/typescript/packages/reality-data-client)
