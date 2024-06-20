<!-- Copyright (c) Bentley Systems, Incorporated. All rights reserved.            -->
<!-- See LICENSE in the project root for license terms and full copyright notice. -->

# OAuth2 authorization

## Overview

Bentley iTwin APIs and SDKs require the end user to give consent to your application to retrieve and use data on user&#39;s behalf. Our APIs use OAuth 2.0 to allow applications access to the data. The following instructions contain information on how to setup your application to use OAuth 2.0. You can find the detailed specification for OAuth 2.0 at [rfc6749](https://tools.ietf.org/html/rfc6749).

Before you can begin the OAuth process, you must first register a new app with the iTwin Platform. When registering a new app, you will need to provide basic information including the application name, and redirect URI to be used for redirecting users back to the appropriate web server / browser / native app. If you haven&#39;t already, click [here](https://developer.bentley.com/register) to register a new application before proceeding.

## Key terminology

The following key terms are important to know when using OAuth 2.0:

Access Token – a token which contains a string that can be used to make authenticated requests to an API to access protect resources. The string has no meaning to the application using it, but represents that the user has authorized the application to access their account. The token is bounded by an appropriate lifetime, scopes, and other information that the server may require.

Authorization Server – the authorization server validates the identity of the user and then issues access tokens to the app to grant access to protected resources on the user&#39;s behalf.

Client – an application which is attempting to access protected resources on behalf of the resource owner (such as the end user). The client can be hosted on a server, desktop, or mobile device.

Client ID – a unique public identifier for an app.

Client Secret – a random string that is known only to the application and the authorization server. The client secret is required for authorizing confidential clients for preventing the authorization server from providing tokens to rogue apps.

Confidential Client – Clients which have the ability to maintain the confidentiality of the Client Secret. Typically, these clients run on a server under the control of the developer, where the source code and configuration is not accessible to users (web server application).

Public Client – Clients that do not have the ability to maintain the confidentiality of the Client Secret. Mobile, desktop and browser apps are typically considered public clients. In all of these cases, the secret should not be used because it can be easily discovered by other developers.

Redirect URI – the Redirect URI is used by the authorization server to redirect the user back to the application with authorization code after the user has successfully authorized the app.

Refresh Token – a token which contains a string that can be used to get a new access token (and optionally a new refresh token) when the current access token expires. A refresh token is needed for making authorized requests without user interaction (for background jobs or long-running tasks). Refresh token is requested with a special "offline_access" scope, and such a request will always present a permissions consent page for end user.

Scope – OAuth 2.0 scopes provide a way to limit the amount of access that is granted to an access token. This can include limiting which protected resources can be access and what level of access (i.e. READ / WRITE) is granted. If a client tries to call an API endpoint and does not include the appropriate scopes, the call will fail with a 401 Unauthorized response.

## Authorizing web applications

Web apps are written in a server-side framework and run on a server where the source code or configuration of the application is not available to the public. This allows the use of a client secret when communicating with the authorization server to help improve security.

**NOTE:** Your client credentials carry many privileges, so be sure to keep them secure!

- Do not put your client credential information (clientid, client secret or access tokens) in publicly accessible code where they can be discovered.
- Store them in a safe place on the backend (server).

### Authorization code flow

Most Bentley APIs support the OAuth 2.0 Authorization Code Flow. This flow provides the ability for a resource owner (owner of the data to access) to authorize applications to access their personal data on their behalf. Your application can use this flow including all built-in features like customer login and consent handling in order to get the authorization by the resource owner.

To understand how this flow works, please see the [authorization code flow](/tutorials/authorize-webapp/#user-authorization-code-flow) section of the [authorize a web application](/tutorials/authorize-webapp/) tutorial. We recommend following the full tutorial to understand the steps involved in obtaining authorization.

## Authorizing single-page applications (SPA) and desktop/mobile applications (native)

Native and single-page applications are public clients without a dedicated backend server. The implication of this is that these application types cannot securely store a client secret.

- In a native application, the code can be decompiled to reveal the client secret, which is bound to the app and is the same for all users and devices.
- In the case of a single page application, the client secret cannot be stored securely because the entire source is available to the browser.

### Authorization code flow with Proof Key for Code Exchange (PKCE)

In order to mitigate these security risks, OAuth 2.0 provides an option for Proof Key for Code Exchange (PKCE) by OAuth Public Clients (see OAuth 2.0 [RFC 7636](https://tools.ietf.org/html/rfc7636)). PKCE allows the calling application to dynamically generate a random, one-time key called a &quot;code verifier&quot;. Additionally, the calling app creates a transform of the &quot;code verifier&quot; called the &quot;code challenge&quot; and sends it to the authorization server when obtaining an authorization code.

The authorization code obtained is then sent to the token endpoint with the &quot;code verifier &quot;and the server compares it with the previously received &quot;code challenge&quot; so that it can perform the proof of the &quot;code verifier&quot; by the client application. This provides a mitigation as the &quot;code verifier&quot; would be unknown to the attacker and cannot be intercepted as it is sent over TLS.

To understand how this flow works, please see the [authorization code flow](/tutorials/authorize-native/#user-authorization-code-flow) section of either the [authorize a single-page application](/tutorials/authorize-spa/) or [authorize a native application](/tutorials/authorize-native/) tutorial. We recommend following the full tutorials to understand the steps involved in obtaining authorization.

## Using refresh tokens

Web applications and native applications can request a refresh token for making authorized requests without user interaction (for background jobs or long-running tasks). To receive a refresh token, you need to request an additional scope "offline_access" in the authorization request. See step 1 of obtaining an access token section in either the [authorize a web application](/tutorials/authorize-webapp/#request-a-new-access-token-with-a-refresh-token) or [authorize a native application](/tutorials/authorize-native/#request-a-new-access-token-with-a-refresh-token) tutorial for more details of how to pass this scope.

When the "offline_access" scope is passed, the response from the authorization server will include both an access token and a refresh token.

When the access token expires, you can use the refresh token in order to obtain a new access token. This way it is not required to request a new authentication/consent from the end user. In addition to the refresh token your client must authenticate using the HTTP Basic method again.

Our authorization server will give you a new OAuth access token together with a new refresh token.

## Authorizing service (machine-to-machine)

Service apps are designed to operate without user interaction (sometimes called two-legged OAuth) in order to access web-hosted resourced by using the identity of an application. Services run on a server where the source code or configuration of the application is not available to the public. This allows the use of a client secret when communicating with the authorization server to help improve security.

**NOTE:** Your client credentials carry many privileges, so be sure to keep them secure!

- Do not put your client credential information (clientid, client secret or access tokens) in publicly accessible code where they can be discovered.
- Store them in a safe place on the backend (server).

The service app type does not represent any user or organization and does not have access to anything by default. If you want to provide access to projects for that application, you need to invite it to the projects using client email, provided in App details page.

### Client credential flow

The Client Credential flow provides the ability for a web service (confidential client) to use it&#39;s own credentials, instead of impersonating a user, to authenticate when calling a web service. Permissions are granted directly to the application itself by an administrator. When the app presents a token to a resource, the resource enforces that the app itself has authorization to perform an action since there is no user involved in the authentication.

To understand how this flow works, please see the [client credentials flow](/tutorials/authorize-service/#client-credential-flow) section of the [authorize a service application](/tutorials/authorize-service/) tutorial. We recommend following the full tutorial to understand the steps involved in obtaining authorization.

## Error responses

The Authorization Server provides standard HTTP status response codes in the response header.

- A 2xx type response typically represents a successful response.
- A 4xx type response typically represents a client error.
- A 5xx type response typically represents a server error.

The following errors may occur when submitting a request for an access token:

- 400 – Bad request. Common causes include:
  - The given authorization code is not valid or was already used.
  - The redirect_uri differs from the one registered for your client..
- 401 – Unauthorized. Common causes include:
  - The specified client ID is invalid.
  - The token is not valid (has expired).
- 403 – Forbidden. The client down not have access rights to the resource.
- 429 – Too many requests. The application&#39;s rate limit for the resource has been exhausted.
- 500 – Internal Server Error. This is typically indicative that the endpoint is temporarily unavailable.
- 502 – Bad Gateway. This indicates that the server got an invalid response.

Other OAuth protocol errors can be returned to redirect_uri in an &quot;error&quot; parameter:

- invalid_request - The request is missing a required parameter, includes an invalid parameter value, includes a parameter more than once, or is otherwise malformed.
- unauthorized_client - The client is not authorized to request an authorization code using this method.
- access_denied - The resource owner or authorization server denied the request.
- unsupported_response_type - The authorization server does not support obtaining an authorization code using this method.
- invalid_scope - The requested scope is invalid, unknown, or malformed.
