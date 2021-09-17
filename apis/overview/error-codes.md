<!-- Copyright (c) Bentley Systems, Incorporated. All rights reserved.               -->
<!-- See LICENSE.md in the project root for license terms and full copyright notice. -->

# HTTP Error Codes

The APIs return standard HTTP client error codes.

| HTTP error code          | Description                                                                                    |
| ------------------------ | ---------------------------------------------------------------------------------------------- |
| 400 Bad request          | The request is invalid.                                                                        |
| 401 Unauthorized         | The request lacks valid authentication credentials.                                            |
| 403 Forbidden            | This user does not have the required permissions to access the resource.                       |
| 404 Not found            | The requested resource could not be found.                                                     |
| 409 Conflict             | The request could not be processed because of a conflict in the current state of the resource. |
| 413 Payload Too Large    | The request is larger than the server is willing or able to process.                           |
| 422 Unprocessable Entity | The request was well-formed but was unable to be followed due to semantic errors.              |
| 429 Too Many Requests    | The client has sent too many requests in a given time period.                                  |
