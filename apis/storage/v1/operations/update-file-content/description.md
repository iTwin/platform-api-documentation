---

Update file's content

### Notes

File update is three steps operation. This request creates hyperlinks for file content update and confirmation. Next two requests need to be executed by using links from the response. Maximum file size to upload with single request is **256 MiB**. If bigger files needs to uploaded there are possibility to use Azure libraries or by uploading file with [multiple requests](https://docs.microsoft.com/en-us/rest/api/storageservices/operations-on-block-blobs).

- **uploadUrl** is required for file upload. Upload can be done by sending http request and specifying x-ms-blob-type header to BlockBlob.
- **completeUrl** should be used to confirm file upload and it is final request for file creation.

{!Authorization.md!}

{!RbacPermissions.md!}

---