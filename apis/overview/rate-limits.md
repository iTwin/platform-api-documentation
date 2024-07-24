<!-- Copyright (c) Bentley Systems, Incorporated. All rights reserved.            -->
<!-- See LICENSE in the project root for license terms and full copyright notice. -->

# Rate limits and quotas

Bentley cloud services are used by many applications. We define rate limits and quotas for our APIs in order to make sure that they perform well for all applications. The limits indicate how many times an application can call an API or endpoint within a given time period. The limits are designed to be reasonable for normal operation while limiting abusive applications.

## Rate limits - general

In most cases, rate limits are determined by the iTwin Platform subscription associated with the OAuth client that the client application is using. Please also note that in addition to a rate limit, Trial subscriptions also have a cap of 5000 calls per hour.

**Rate limits by subscription**:

| Subscription tier | Number of requests | per time period |
| ----------------- | :----------------: | :-------------: |
| Trial             |        500         |     minute      |
| Basic             |        5000        |     minute      |
| Premium           |        5000        |     minute      |
| Custom            |        5000        |     minute      |

## Rate limits - API-specific

APIs may further restrict the number of requests allowed in a given time period. This will generally be done only on specific operations but can apply to an entire API. Please look for this information as part of the API's `Reference` documentation.

## Programmatically determine rate limit information

In your application or service, you may want to be able to gracefully handle a request that is rejected due to exceeding a rate limit. There are a few different possibilities that one may encounter here. This guide should cover the majority of cases.

### Rate limited by the iTwin Platform

When a rate limit is encountered, a [HTTP 429 - Too Many Requests](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/429) response will be returned. In addition to the standard `Retry-After` response header, some additional headers will be added to aid you in understanding why the rate limit occurred. You could, for example, use this information to provide custom messaging in your UI or use it in log messages.

| Header name                                 | Description                                                                            |
| ------------------------------------------- | -------------------------------------------------------------------------------------- |
| iTwinPlatform-RateLimit-RemainingCalls      | Number of requests allowed before reaching the rate limit                              |
| iTwinPlatform-RateLimit-Retry-After-Seconds | After reaching the limit, the number of seconds to wait before retrying the request    |
| Retry-After                                 | HTTP standard header. Value is the same as that of ITwinPlatform-RateLimit-Retry-After |
| iTwinPlatform-Tier                          | The name of the subscription used to make the request                                  |

### Rate limited by a service on which the API depends

APIs may depend on additional services. Ideally, the API reference documentation should take this into account and document the strictest rate limit of any service upon which it depends. If you are reading this section of the documentation, you probably already know that services upon which one is dependent may change. We will always strive to keep documentation about rate limits up-to-date. However, we would encourage you to also rely on the standard `Retry-After` header in your application/service. If you encounter a rate limit and find that documentation about it is incorrect or missing, please [let us know](/support).
