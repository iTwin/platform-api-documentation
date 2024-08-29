---

Runs the specified ExportConnection.

### Notes

1. The export process usually takes time and is performed in the background. For that, we need to store the user's refresh token. The refresh token needs to be stored before calling the 'Create ExportConnection Run' end-point. You can get authorization information by using [Get Authorization Information API](https://developer.bentley.com/apis/export/operations/get-authorizationinformation/). This API will return the current status and a redirect URL if the token has to be renewed.

2. When a run is successfully created, the operation returns HTTP status code 202/accepted - the request is accepted for processing and will execute in background. The response will include a location header pointing to the created run. If an existing active run already exists for the iModel, a new run is not initiated, instead 303/see other is returned along with location header pointing to that existing active run. 
In the rare event that multiple create run requests are being made simultaneously, only the first request is processed and 409/conflict is returned for others.

{!Authorization.md!}

---