---

Returns the primary Account for the calling user. 

When a user creates a new iTwin, it will be created in the primary Account unless specified otherwise.

If a user is associated with an Organization, that user will be able to query for any Account iTwin owned by their Organization. If the Organization has more than one Account then the MyPrimaryAccount endpoint will return only the primary Account for that Organization. Other Accounts can be queried using the [Get My iTwins](https://developer.bentley.com/apis/itwins/operations/get-my-itwins/) endpoint with the subClass=Account parameter.

If a user is not associated with an Organization, then a single Account iTwin will be created for the user. The MyPrimaryAccount endpoint will return that Account.

{!Authorization.md!}

---
