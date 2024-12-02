---

Requests that anywhere from 1 to 5 issues be exported to a file and saved in cloud-based storage (accessible through the Storage API). Currently 'pdf' is the only supported file type. The IDs of the issues must be specified in a query string parameter named "ids", separated by commas if there is more than one. A sample request URL that exports 3 issues to a PDF is as follows--

https://api.bentley.com/issues/exportPdfToStorage?ids=abab23524535,89458jjlij,32636wtewtwt&folderId=090909877987&includeHeader=true

Note that unlike most GET requests, this is not an idempotent operation; each time it is called, a new file will be generated. The response will not contain the file itself, but links to download it from Storage.

All issues specified in the request must come from the same iTwin, or the request will fail. The client may also specify the ID of a destination folder where the file should be saved; otherwise, it will be saved in the iTwin's root folder.  They can also specify whether to include a textual header with issue metadata at the top of each page (default) or exclude it.

{!Authorization.md!}

---