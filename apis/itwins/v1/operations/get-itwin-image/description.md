---

Gets the image metadata for the specified iTwin. 

The metadata will contain the name of the image and a URL for downloading the image. The name of the image is unique and will only change if the image changes. It can be used as a long term cache key to determine if you have already downloaded the image. The URLs will be valid for a minimum of 1 hour.

This API is used to get a link to the small image and the original uploaded image. To make it easier to use the small image as a thumbnail, the small image link is also included as a property on every iTwin.

{!Authorization.md!}

{!iTwinMemberOfAuthorization.md!}

---