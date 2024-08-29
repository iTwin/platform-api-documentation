---

This endpoint is used to run the transformation based on an already created configuration. Sending a post request will submit a background processing job that is able to report progress back to the same transformation instance that you can query by the transformation ID.

First run of the transformation will process the whole source iModel and push data to the target iModel. 
Only one transformation job can run on the same target iModel at the same time.
Consecutively submitted jobs for the same configurationId will only process changes to the source iModel.

{!TransformationStatus.md!}

{!Authorization.md!}

{!iModelsPermissions.md!}

{!RateLimits.md!}

{!TransformationElementLimiting.md!}

---
