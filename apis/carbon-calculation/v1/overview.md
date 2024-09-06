## Carbon Calculation

Our Carbon Calculation APIs provide integrations for your digital twins into a variety of software tools, provided by both third-parties and Bentley Systems, to assist with environmental impact calculations such as Life Cycle Assessments (LCA) or Embodied Carbon estimations (EPD).

### Integrations - EC3 & One Click LCA

For environmental impact calculations, iTwin Platform is integrating with LCA software partners such as EC3 & One Click LCA. Bentley's iTwin Platform integration with EC3 & One Click LCA allows you to take Quantity Takeoff reports created using the iTwin Reporting Platform and export them to EC3 or One Click LCA for convenient Life Cycle Analysis for both infrastructure projects and buildings. The iTwin Platform enables aggregation of engineering data created by various design tools. A summary of the design data is exported through this integration, allowing you to gain insights into the environmental impacts of your infrastructure projects.

For all workflows, first you will need a report. For guidance on creating a report, see [iTwin Reporting Platform](/apis/insights) documentation. Detailed below, each integration has additional requirements that must be fulfilled during report configuration on top of standard iTwin Reporting Platform procedures.

### EC3

Embodied Carbon in Construction Calculator ([EC3](https://buildingtransparency.org/ec3)), a free database of construction EPDs and matching building impact calculator for use in design and material procurement. EC3 is built by [Building Transparency](https://www.buildingtransparency.org/) with a core mission to provide the open access data and tools necessary to enable broad and swift action across the building industry in addressing embodied carbon's role in climate change.

> An account with EC3 is required to use this integration. User accounts are created at [EC3](https://buildingtransparency.org/auth/register). For guidance on EC3, please contact [EC3 support](https://www.buildingtransparency.org/about/contact-us/).

[Prepare a report](/apis/insights). The Report and associated Mapping should contain all quantities relevant to your desired carbon calculation and the material. EC3 uses material as a lookup to find the embodied carbon constants for each element.

When ready with the report, [acquire an access token from EC3 using their APIs](https://buildingtransparency.org/ec3/manage-apps/api-doc/guide#/2._Accessing_API/authentication.md).

Next you must setup your EC3 upload configuration. See [Create EC3 Configuration](/apis/carbon-calculation/operations/create-ec3-configuration) for futher information. Our API allows you to manage and store multiple configurations that can be reused as necessary. Finally, export your report to EC3. See [Create EC3 Job](/apis/carbon-calculation/operations/create-ec3-job). Use the [Get EC3 Job Status](/apis/carbon-calculation/operations/get-ec3-job-status/) endpoint to monitor export progress.

Once the export is complete, visit the EC3 portal to view the results.

### One Click LCA

[One Click LCA](https://www.oneclicklca.com) is a third-party construction LCA and EPD software company. Bentley's iTwin platform integration with One Click LCA allows you to take Quantity Takeoff reports created using the iTwin Reporting platform and export them to One Click LCA for convenient Life Cycle Analysis for both infrastructure projects and buildings. The iTwin Platform enables the incorporation of engineering data created by various design tools. A summary of the design data is exported through this integration, allowing you to gain insights into the environmental impacts of your infrastructure project. This integration also allows you to work with the third party certifications and standards listed in [Life Cycle Assessment software for BREEAM, LEED, DGNB and more](https://oneclicklca.com/software/design-construction/certifications-compliance).

> An account with One Click LCA is required to use this integration. User accounts are created at [One Click LCA](https://oneclicklcaapp.com/app/register). For guidance on One Click LCA, please contact One Click LCA support: support@oneclicklca.com.

[Prepare a report](/apis/insights). The Report and associated Mapping should contain all the elements and required properties of One Click LCA's Life Cycle Analysis.

Uploading your report to One Click LCA can be done using our [sample UI package](https://www.npmjs.com/package/@itwin/one-click-lca-react). Follow the pacakge instructions to set up a UI-driven workflow for uploading your digitial twin data to One Click LCA. If you need to implement something custom, read on.

When ready with the report, acquire an access token from One Click LCA using their APIs. A user token is acquired by sending a POST request to `https://oneclicklcaapp.com/app/api/login` with request body:

```json
{
  "username": "username",
  "password": "password"
}
```

> Creating a bearer token requires having a valid user account and a license for One Click LCA.

Finally, export your report to One Click LCA. See [Create a One Click LCA Job](/apis/carbon-calculation/operations/create-oneclicklca-job/) for further information. This may take some time. Use the [Get One Click LCA Job Status](/apis/carbon-calculation/operations/get-oneclicklca-job-status/) endpoint to monitor export progress. You can also use the [@itwin/insights-client](https://www.npmjs.com/package/@itwin/insights-client) NPM package to send these requests.

Once the export is complete, return to the One Click LCA portal to view results.

## Client Packages

Open source Typescript client packages are available for the Carbon Calculation API:

- @itwin/insights-client - [NPM registry](https://www.npmjs.com/package/@itwin/insights-client)
- @itwin/one-click-lca-react - [NPM registry](https://www.npmjs.com/package/@itwin/one-click-lca-react)
- @itwin/grouping-mapping-widget - [NPM registry](https://www.npmjs.com/package/@itwin/grouping-mapping-widget)

## Media Links

Additional information can be found here:

- Creating and Sharing Insights with the iTwin platform - [YouTube](https://www.youtube.com/watch?v=6MhEm6cTOqY)
- Decluttering your Digital Twin - [Medium](https://medium.com/itwinjs/decluttering-your-digital-twin-9000bd017f50)
- Bentley Systems and ZERO Construct showcase a new integration between the iTwin Platform and One-Click LCA - [Bentley On24](https://event.on24.com/wcc/r/3848641/BE096C05AFAE34EFC0CCF96008D1D2ED)
