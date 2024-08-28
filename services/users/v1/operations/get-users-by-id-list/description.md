This API allows you to pass a list of user ids and get back the user metadata for each one. It is implemented as a POST so that the ids can be specified in the body instead of the url. This allows you to specify up to 1000 user ids.

This API will only return metadata for users that are in the same organization as the caller.

{!Authorization.md!}

{!RateLimits.md!}
