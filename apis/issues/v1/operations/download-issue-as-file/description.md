---

Gets the specified issue exported to the specified file format. Currently, the default--and only supported format--is PDF. The issue with the specified ID will be laid out in the PDF according to its associated form definition.

The generated PDF will have a header at the top of each page with metadata about the issue (such as its name and creation date) unless the 'includeHeader' query parameter is set to false.

{!Authorization.md!}

---