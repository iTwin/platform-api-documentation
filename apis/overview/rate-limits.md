<!-- Copyright (c) Bentley Systems, Incorporated. All rights reserved.            -->
<!-- See LICENSE in the project root for license terms and full copyright notice. -->

# Rate limits and quotas

Bentley cloud services are used by many applications. We define rate limits and quotas for our APIs in order to make sure that they perform well for all applications. The limits indicate how many times an application can call an API or endpoint within a given timeframe. The limits are designed to be reasonable for normal operation while limiting abusive applications. If an application exceeds the rate limit it will receive an HTTP error code 429 "Too Many Requests". The error response includes a Retry-After header that indicates how long clients should wait before retrying.

The iTwin Platform APIs which are in Technology Preview have a rate limit of 50 API calls per minute and a quota of 500 API calls per hour.
