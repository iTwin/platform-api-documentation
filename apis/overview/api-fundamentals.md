<!-- Copyright (c) Bentley Systems, Incorporated. All rights reserved.            -->
<!-- See LICENSE in the project root for license terms and full copyright notice. -->

# API Fundamentals

## Schema

All API access is over HTTPS and is accessed from https://api.bentley.com/. All data is sent and received as JSON.

Dates and times use ISO 8601 format.

    YYYY-MM-DDTHH:MM:SSZ

## Pagination

APIs that return collections could return a partial set of results and clients need to page through the results to retrieve all of the results. Requests that return multiple items will be paginated to 1,000 items by default unless specified otherwise in an API operation's documentation.

Clients can use the optional **$top** and **$skip** query parameters to specify the number of results to return and an offset into the collection. If both parameters are provided the server will apply the **$skip** parameter first and then the **$top** parameter.

The server will attempt to use the values specified by the client but clients should be prepared to handle responses that contain a different page size. If the server can't support the given **$top** or **$skip** parameters it will return an error.
