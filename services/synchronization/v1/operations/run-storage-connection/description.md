---

Runs the specified StorageConnection.

### Notes

When a run is successfully created, the operation returns HTTP status code 202/accepted - the request is accepted for processing and will execute in background. The response will include a location header pointing to the created run. If an existing active run already exists for the iModel, a new run is not initiated, instead 303/see other is returned along with location header pointing to that existing active run. 
In the rare event that multiple create run requests are being made simultaneously, only the first request is processed and 409/conflict is returned for others.

{!Authorization.md!}

---