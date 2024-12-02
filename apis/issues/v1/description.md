Issue Service

View, create, and edit details of issues that have been raised in an iTwin or project, as well as their comments, attached files, and change history.  Retrieval of form definitions (which define how to display an issue in an interactive UI) is also supported, though customization of them is not, and should be done by a project administrator through the CONNECT Issues web application, if needed. This form-editing app can be found at https://connect-formmanager.bentley.com/designer/#/your-itwin-id where `your-itwin-id` is replaced by the ID of the iTwin or project you're creating custom forms for.

## Limits

All API calls that return a list of results will return a maximum of 50 results. Some endpoints support a `$top` parameter to specify a number of results to retrieve (up to the maximum) and a `continuationToken` parameter to continue paging through results, allowing access to results beyond the first 50. These parameters will be included in the documentation for those endpoints.

Clients with a Developer, Partner, or Integrator subscription will be limited to 5000 requests per minute. Clients with a Trial subscription will be limited to 500 requests per minute.