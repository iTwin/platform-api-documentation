---

Retrieves the text and metadata for all comments that have been posted to the given issue. If the Prefer header was specified with the value "return=representation", the response will include the email address of each comment author, though this may incur additional processing time.  If there is an extraordinarily large number of comments, only 50 distinct user email addresses will be retrieved and shown. Regardless of the Prefer header value, the "_links" object associated with each comment will provide a link to additional information about the comment author.

### Permissions

To use this endpoint, the user is required to have the Forms **View** (`Forms_ViewAccess`) permission for the iTwin, or for the issue's associated form definition if form definition security is specified. (Having any other level of Forms permission automatically grants the **View** permission as well.)

{!Authorization.md!}

---