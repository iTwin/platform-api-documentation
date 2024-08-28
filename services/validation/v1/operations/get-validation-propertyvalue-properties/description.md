---

Gets the properties matching a filter string for the latest named version of an iModel. This request relies on a previous call to start schema extraction on an agent. Since this extraction completes asynchronously, the user can send this request periodically until a status of 'available' is returned in the response.

- Discover iModel ids by calling [GET /imodels](/api-groups/data-management/apis/imodels/operations/get-project-imodels/)

- Extract iModel schemas by calling [POST /clashdetection/schemas/imodels](/api-groups/validation/apis/clash-detection/operations/extract-schema-info/)

{!Authorization.md!}

---