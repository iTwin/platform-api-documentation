## Forms API

The Forms service lets project members collect a variety of data through filling out customizable forms. Project administrators can design forms for capturing meeting minutes, daily work logs, asset and site observation results, and more. Project members can then fill out these forms while working in the field. Like an issue, a form can be assigned to a particular user and can move through statuses in a workflow as work on it is completed.

The Forms REST API provides access to the raw data entered into these forms, including the ability to read and set field values, attached files, and comments, as well as view the audit trail (history) of a particular filled-out form.

### Limits

All Forms API calls that return a list of results will return a maximum of 50 results. Some endpoints support a `$top` parameter to specify a number of results to retrieve (up to the maximum) and a `continuationToken` parameter to continue paging through results, allowing access to results beyond the first 50. These parameters will be included in the documentation for those endpoints.

Clients with a Basic, Premium, or Enterprise subscription will be limited to 5000 requests per minute. Clients with a Trial subscription will be limited to 500 requests per minute and 5000 per hour.
