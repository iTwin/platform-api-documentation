---

Uploads a design file to create a digital component.

### Notes

This endpoint is to create a component from design file. Supported file extensions are '.rfa', '.dgn' and '.cel'. This is a long running activity
that runs in background after the endpoint is called and creates a component by extracting information from the design file, e.g., category,
application, manufacturer and other metadata found in the design file. Response object has links to upload the design file or type catalog file, if
specified. Client must upload type catalog file before uploading design file. Once files are uploaded, component creation activity can be tracked
using job endpoint returned in the 'Location' header. Once job succeeds, component can be fetched using 'component' property provided under _links
in job endpoint response.

### Referenced Entities
A component can have referenced entities, e.g catalogs. These values should be valid Ids of existing entities.

{!Authorization.md!}

{!LibraryPermissions.md!}

{!RateLimits.md!}

---