---

Create new file

### Notes

File creation is three steps operation. This request will create file's meta data. Next two requests need to be executed by using links from the response. Maximum file size to upload with single request is **256 MiB**. If bigger file needs to be uploaded there are possibility to use Azure libraries to upload file via given Azure SAS url or by uploading file with [multiple requests](https://docs.microsoft.com/en-us/rest/api/storageservices/operations-on-block-blobs).

- **uploadUrl** is required for file upload. Upload can be done by sending http request and specifying x-ms-blob-type header to BlockBlob.
- **completeUrl** should be used to confirm file upload and it is final request for file creation.

{!Authorization.md!}

{!RbacPermissions.md!}

### Errors

This request can return InvalidCreateFileRequest error with 422 status code. This could happen because of these reasons:

- File name contains invalid characters.
- File name's length is larger than 255 characters.
- File could be harmful. For example, executable files are not accepted.

---