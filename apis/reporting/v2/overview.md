## Reporting and Insights

The Reporting API is a tool for aggregating digital twin data from multiple sources into one unified format and place. With the Reporting API, consuming your data through business intelligence applications such as Power BI or your own custom-built application is dramatically simplified.

### Mapping

The Reporting story begins with [Mapping](/apis/insights/operations/create-mapping/). Mapping is a configuration process where all desired data sources are identified. These Mappings also will help describe what data is desired from each data source and how to structure it for Reporting. The Mapping process will be unique for each type of data source. For example, a Mapping for data from an iModel may not look the same as a Mapping for data from Validation, but ultimately all that data needs to arrive at one place and that is what Mapping orchestrates for you.

### Reports

A Report represents a collection of data. The way the Reporting API views a Report is as a collection of Mappings. With the Reporting API, you will assign one or more Mappings to a Report to be consumed by some application such as Power BI as a single data source.

### Extraction

More often than not, some preprocessing will be required before data defined in a Mapping is actually available to be consumed as a Report. Endpoints are provided in the Reporting API to trigger the data extraction process. Depending on the data source this may be a one-time action, required for data syncs, or not required at all. See data source specific documentation to find out more.

### Data Access

Accessing the resulting data is done using a set of OData v4 endpoints. Any application that can use the OData protocol such as Power BI will automatically understand how to fetch your Report data. Access to data can either follow the standard Bearer Token authorization shared with all other Reporting APIs, or use Basic Authentication with the credentials and keys provided via the [Create ApiKey](/apis/insights-v2/operations/create-apikey/) operation.

### Typical Workflow

_Described for an iModel data source. Some variation may exist for other data sources._

- Create an empty iModel [Mapping](/apis/insights/operations/create-mapping/).
- Create one or more [Groups](/apis/insights/operations/create-group/) under that Mapping. A Group is a collection of iModel elements defined by a query.
- Create one or more [Group Properties](/apis/insights/operations/create-groupproperty/) for each Group. These are the properties to be extracted from the iModel elements and how they should be identified in your Report.
- Create a new [Report](/apis/insights-v2/operations/create-report/).
- Assign the Mapping created to the new Report ([Report Mapping](/apis/insights-v2/operations/create-report-mapping/)).
- Run the [iModel Extraction](/apis/insights-v2/operations/run-extraction/).
- Ensure the Extraction has completed.
- Create a new [ApiKey](/apis/insights-v2/operations/create-apikey/).
- Connect an OData v4 compliant application to the Report using the generated `apiKey`.

## Client Packages

Open source Typescript client packages are available for the Reporting API:

- @itwin/insights-client - [NPM registry](https://www.npmjs.com/package/@itwin/insights-client)
- @itwin/grouping-mapping-widget - [NPM registry](https://www.npmjs.com/package/@itwin/grouping-mapping-widget)

## Media Links

Additional information can be found here:

* Creating and Sharing Insights with the iTwin platform - [YouTube](https://www.youtube.com/watch?v=6MhEm6cTOqY)
* Decluttering your Digital Twin - [Medium](https://medium.com/itwinjs/decluttering-your-digital-twin-9000bd017f50)