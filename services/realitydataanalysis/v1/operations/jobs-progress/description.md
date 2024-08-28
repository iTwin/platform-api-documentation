---

Retrieve job progress.

### Parameters

The job id

### Remarks

The job progression is deemed valid when the job is active and won't be available after 30 days.

Client should query with a backoff intervals [15,30,60,120] seconds. The interval between the first and second query is 15 sec and then 30 sec... If the percentage changes the sequence is restarted.

{!Authorization.md!}

---
