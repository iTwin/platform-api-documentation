---

### Job Creation

Creates a comparison job. The comparison will be queued when first created and will progress to completion. When completed, you can use [Get Comparison Job](operations/get-comparison-job/) to query the results.

### Webhooks

Once a job is finished, an event is triggered via the [Webhooks API](https://developer.bentley.com/apis/webhooks-v2/overview/). All subscribers of the [changeElements.jobCompleted.v1](https://developer.bentley.com/apis/webhooks-v2/available-events/#Changed%20Elements-events-ref) event type will be notified.

{!Authorization.md!}

---
