## Issues Resolution API

Issues Resolution provides a central repository where you can easily manage, assign, and track the progress of all project issues. Team members can communicate issues from the field to give project managers insight into issues so they can alert appropriate project participants to immediate action.

An issue includes a subject, description, assignee, and status. Comments can be added to an issue and they can be used to communicate among project team members. Additional information like files, saved views, and markups can be attached to an issue. The audit trail provides the history of all the changes to an issue.

The Issues API provides the ability to manage issues, comments, attachments, and audit trails.

### Limits

All Issues API calls that return a list of results will return a maximum of 50 results. Some endpoints support a `$top` parameter to specify a number of results to retrieve (up to the maximum) and a `continuationToken` parameter to continue paging through results, allowing access to results beyond the first 50. These parameters will be included in the documentation for those endpoints.

Clients with a Basic , Premium, or Enterprise subscription will be limited to 5000 requests per minute. Clients with a Trial subscription will be limited to 500 requests per minute and 5000 per hour.
