---

Retrieves file

### Notes

This endpoint returns 302 status code with Location header, which on success contains a link to the file. Redirection is not supported by developer portal and an error could be returned while using the "Try it" feature for this API. However, this endpoint will work if a request is sent from a different http client or by using the link specified in the response Location header.

{!Authorization.md!}

{!RbacPermissions.md!}

---