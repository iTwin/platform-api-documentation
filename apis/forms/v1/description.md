Forms Service

View, create, and edit details of forms that have been filled out for an iTwin/project, as well as their comments, attached files, and change history.  Full CRUD functionality is available for form data, with form definitions being available in a read-only context.

Note that throughout this API the terms "form" (by itself) and "form data" both refer to the same thing: data collected from users (generally entered into controls of a UI, or programmatically generated). By contrast, a "form definition" is a piece of metadata connected to form data instances. It determines the "type" of form that is filled out, and in applications that support custom form layouts, it determines how the controls are placed in the user interface.

Form definitions should be added, imported, and customized by project administrators through the Bentley Form Manager web application; they cannot be modified using this API. The app can be found at https://connect-formmanager.bentley.com/designer/#/your-itwin-id (replace `your-itwin-id` with the ID of the actual iTwin or project whose form definitions you want to customize).

## Limits

All API calls that return a list of results will return a maximum of 50 results. Some endpoints support a `$top` parameter to specify a number of results to retrieve (up to the maximum) and a `continuationToken` parameter to continue paging through results, allowing access to results beyond the first 50. These parameters will be included in the documentation for those endpoints.

Clients with a Developer, Partner, or Integrator subscription will be limited to 5000 requests per minute. Clients with a Trial subscription will be limited to 500 requests per minute.