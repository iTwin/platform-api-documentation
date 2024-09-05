---

Uploads an image for the specified iTwin. Maximum supported size is 5 megabytes.

A small, thumbnail image will be automatically generated based on the uploaded image. For convenience, the link to this thumbnail is also returned in the 'image' property on the iTwin.

Upload the image by adding a binary stream to the request body. You must specify the Content-Type header as either image/png or image/jpeg.

 C# Example:
 ```
 var stream = File.OpenRead("c:/test.jpg");
 var streamContent = new StreamContent(stream);
 streamContent.Headers.ContentType = new MediaTypeHeaderValue ("image/jpeg");
 var response = await httpClient.PutAsync($"{iTwinId}/image", streamContent);
 ```
		
{!Authorization.md!}

### Authorization
The user must have the `itwins_modify` permission on the iTwin in order to add an image to the iTwin.

An Organization Administrator can modify any iTwins owned by their Organization. This allows Organization Administrators to upload an iTwin image.

{!iTwinAdminOnlyAuthorization.md!}

---