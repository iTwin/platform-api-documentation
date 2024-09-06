# Grouping and Mapping API

The Grouping and Mapping API is a tool for reimagining your iModel data in a more concise, precise, and optimized representation for any variety of downstream applications. Specific solutions built on top of iModels often do not require the full breadth of the contained data, and different solutions often require redundant configuration steps to filter iModel data down to the needed subset. With the Grouping and Mapping API you can define any number of Mappings, Groups, and Properties as a one-time, reusable configuration that codes a reduced view of the data which can then be reused as configuration across all applicable workflows.

### Mappings

[Mappings](/apis/grouping-and-mapping/operations/create-mapping/) can be seen as logical containers for each ‘reduced view’ - a set of Groups - of iModel data you are interested in. For example, a Mapping could be a set of Groups organizing elements by material or discipline. A Mapping could be a set of Groups with properties crafted for EDP (Environmental Product Declarations) workflows like material and quantity. Mappings are transferable. Once a Mapping is defined, it can be shared across an organization, across all iModels.

### Groups

Each Mapping can contain any number of [Groups](/apis/grouping-and-mapping/operations/create-group/). Each Group defines a different subset of the iModel data. Revisiting the EPD workflow example, a Group can be made for all concrete elements with Properties defined for volume and concrete grade. Another Group can be made for all steel beams with Properties defined for section and length. Continuing this pattern, a generic set of iModel element Groups can be defined that creates an optimized representation of the iModel data for a particular set of use cases. The same Groups defined for EPDs could also be used for other workflows such as generating Procurement reports or whatever else – only limited by the creativity of the user. The tedious configuration task required to know what data to pull from the iModel can be performed once and shared across workflows with this convenient set of APIs.

### Properties

If a Group is thought of as a Table of data, Properties are the Columns. The Grouping and Mapping APIs provide an interface to define a set of Properties for each Group. Properties come in several flavors.

- [Mapped Properties](/apis/grouping-and-mapping/operations/create-property/#mappedproperties) are the most basic. They are derived directly from property data in the iModel. For example, if the element contains a value for volume, it can be mapped to your Group using a Mapped Property.
- [Calculated Properties](/apis/grouping-and-mapping/operations/create-property/#calculatedproperties) can be used to augment the iModel element data. If Group elements are missing various mass properties such as Volume, Area, Length, etc., a Calculated Property can be used which will augment your iModel data by calculating the value for you during Data Extraction.
- Use [Custom Calculations](/apis/grouping-and-mapping/operations/create-property/#customcalculations) if there is a need for even more sophisticated data augmentation. Custom Calculations allow users to define new Properties by writing short code snippets that can use other Properties on the same Group as variables. For example, if a user have access to properties for `volume` and `density`, they could calculate ‘weight’ with a Custom Calculation.

**Note:** Taking full advantage of Calculated Properties and Custom Calculations requires use of the [iTwin Platform Reporting APIs](/apis/insights/overview/) and its Data Extraction workflows. The values of these Properties are not resolved until after Data Extraction is run.

### Typical Workflow

- Present users with an interface to edit Mappings, Groups, and optionally Properties in the context of an iModel. See our react component UI packages for a sample implementation of such an interface.
  - [Sample UI package for Mapping management (@itwin/grouping-mapping-widget) in action.](https://www.itwinjs.org/sandboxes/iTwinPlatform/Grouping%20Mapping%20Widget)
- Users create Mappings and Groups to segment and organize their iModel data.
- If applicable users map or create Properties.
- If your application requires Calculated Properties or Custom Calculations or more streamlined and managed access to Property data, trigger Data Extraction using the [Reporting APIs](/apis/insights/).
- Drive your application(s) using the user’s Group definitions, Property mappings, and extracted Group and Property table data.
  - [Sample application using Groups to visualize iModel elements.](https://www.itwinjs.org/sandboxes/iTwinPlatform/Reporting)

## Client Packages

Open-source TypeScript packages are available for the Grouping and Mapping API:

- @itwin/insights-client – [NPM registry](https://www.npmjs.com/package/@itwin/insights-client)
- @itwin/grouping-mapping-widget – [NPM registry](https://www.npmjs.com/package/@itwin/grouping-mapping-widget)

## Media Links

Additional information can be found here:

- Grouping and Mapping Accreditation Course - [iTwin Platform Accreditation](/learning/courses/grouping-and-mapping/course-intro/course-intro/)
- Creating and Sharing Insights with the iTwin Platform – [YouTube](https://www.youtube.com/watch?v=6MhEm6cTOqY)
- Decluttering your Digital Twin - [Medium](https://medium.com/itwinjs/decluttering-your-digital-twin-9000bd017f50)
