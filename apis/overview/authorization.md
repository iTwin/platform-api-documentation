<!-- Copyright (c) Bentley Systems, Incorporated. All rights reserved.            -->
<!-- See LICENSE in the project root for license terms and full copyright notice. -->

# OAUTH2 AUTHORIZATION

## OVERVIEW

Bentley iTwin APIs and SDKs require the end user to give consent to your application to retrieve and use data on user&#39;s behalf. Our APIs use OAuth 2.0 to allow applications access to the data. The following instructions contain information on how to setup your application to use OAuth 2.0. You can find the detailed specification for OAuth 2.0 at [rfc6749](https://tools.ietf.org/html/rfc6749).

Before you can begin the OAuth process, you must first register a new app with the iTwin Platform. When registering a new app, you will need to provide basic information including the application name, and redirect URI to be used for redirecting users back to the appropriate web server / browser / native app. If you haven&#39;t already, click [here](https://developer.bentley.com/register) to register a new application before proceeding.

## KEY TERMINOLOGY

The following key terms are important to know when using OAuth 2.0:

Access Token – a token which contains a string that can be used to make authenticated requests to an API to access protect resources. The string has no meaning to the application using it, but represents that the user has authorized the application to access their account. The token is bounded by an appropriate lifetime, scopes, and other information that the server may require.

Authorization Server – the authorization server validates the identity of the user and then issues access tokens to the app to grant access to protected resources on the user&#39;s behalf.

Client – an application which is attempting to access protected resources on behalf of the resource owner (such as the end user). The client can be hosted on a server, desktop, or mobile device.

Client ID – a unique public identifier for an app.

Client Secret – a random string that is known only to the application and the authorization server. The client secret is required for authorizing confidential clients for preventing the authorization server from providing tokens to rogue apps.

Confidential Client – Clients which have the ability to maintain the confidentiality of the Client Secret. Typically, these clients run on a server under the control of the developer, where the source code and configuration is not accessible to users (web server application).

Public Client – Clients that do not have the ability to maintain the confidentiality of the Client Secret. Mobile, desktop and browser apps are typically considered public clients. In all of these cases, the secret should not be used because it can be easily discovered by other developers.

Redirect URI – the Redirect URI is used by the authorization server to redirect the user back to the application with authorization code after the user has successfully authorized the app.

Refresh Token – a token which contains a string that can be used to get a new access token (and optionally a new refresh token) when the current access token expires. A refresh token is needed for making authorized requests without user interaction (for background jobs or long-running tasks). Refresh token is requested with a special _offline_access_ scope, and such a request will always present a permissions consent page for end user.

Scope – OAuth 2.0 scopes provide a way to limit the amount of access that is granted to an access token. This can include limiting which protected resources can be access and what level of access (i.e. READ / WRITE) is granted. If a client tries to call an API endpoint and does not include the appropriate scopes, the call will fail with a 401 Unauthorized response.

## AUTHORIZING WEB APPLICATIONS

Web apps are written in a server-side framework and run on a server where the source code or configuration of the application is not available to the public. This allows the use of a client secret when communicating with the authorization server to help improve security.

**NOTE:** Your client credentials carry many privileges, so be sure to keep them secure!

- Do not put your client credential information (clientid, client secret or access tokens) in publicly accessible code where they can be discovered.
- Store them in a safe place on the backend (server).

### Authorization Code Flow

Most Bentley APIs support the OAuth 2.0 Authorization Code Flow. This flow provides the ability for a resource owner (owner of the data to access) to authorize applications to access their personal data on their behalf. Your application can use this flow including all built-in features like customer login and consent handling in order to get the authorization by the resource owner.

These are the steps that the flow executes:

1. Redirect the end user&#39;s (resource owner&#39;s) browser to the authorization server endpoint
1. Authenticate the end user and ask for consent
1. Redirect the end user to your application&#39;s callback URL with an authorization code
1. Exchange the authorization code for an access token
1. Use the access token to call the API on behalf of the end user

<div class="mermaid">
sequenceDiagram
    participant ro as Resource Owner
    participant app as Application
    participant as as Authorization Server
    participant api as iTwin API

    ro->>+app: Connect to application
    app->>+as: Request authorization code
    as->>ro: Redirect to login and consent
    ro->>as: Sign in and consent
    as->>-app: Authorization code
    app->>+as: Exchange authorization code for an access_token
    as->>as: Validate client_id, client_secret, scope and redirect_uri
    as->>-app: Granted access token
    app->>-ro: Signed in

    ro->>+app: Perform action
    app->>+api: API request with the access token
    api->>-app: API response
    app->>-ro: Render content

</div>

The following steps outline how to implement the authorization code flow in your application:

1. Redirect the end user&#39;s browser to the authorization endpoint

    In order to initiate the end user&#39;s authorization, you must redirect the end user&#39;s browser to Bentley&#39;s authorize endpoint. This will provide a login screen to the end user for authentication. After successful authentication, the consent screen is displayed, if the user has not given the consent yet.

    Authorization endpoint: [https://ims.bentley.com/connect/authorize](https://ims.bentley.com/connect/authorize)

    The URL requires the following parameters:

    - response\_type=code: Request an authorization code as the result of the end user authorization process.
    - client\_id=&lt;insert\_your\_client\_id\_here&gt;: Provide the client ID of your application.
    - redirect\_uri=&lt;insert\_redirect\_uri\_here&gt;: This is the callback URL that is registered for you application in order to receive the authorization code.
    - scope=&lt;insert\_scopes\_of\_API\_here&gt;: Include the scopes for the API, which are the permissions to request the end users consent for. For each API, you can find the required scopes in the additional API specific documentation. Please note that you will have to request an additional scope &quot;offline\_access&quot; to receive a refresh token.
    - state=&lt;insert\_client\_state\_here&gt;: (optional) An opaque value used by the client to maintain state between the request and callback. The authorization server includes this value when redirecting the user-agent back to the client. The parameter SHOULD be used for preventing cross-site request forgery.

1. Authenticate the end user and ask for consent

    This step will be performed by Bentley&#39;s authorization server and does not require anything to be implemented in your application.

1. Redirect the end user to your application&#39;s callback URL with an authorization code

    After the end user provides consent for your application, Bentley&#39;s authorization server will redirect the end user with an authorization code to the redirect URL registered with your application.

1. Exchange the authorization code for an access token

    After your application has received the authorization code you can exchange it for an access token. The client must authenticate using the HTTP Basic method and provide the url-encoded clientId and the clientSecret (&lt;insert\_your\_url\_encoded\_client\_id\_here&gt;:&lt;insert\_your\_url\_encoded\_client\_secret\_here&gt;) encoded with BASE64 in the HTTP Authorization header.

    Token Endpoint: [https://ims.bentley.com/connect/token](https://ims.bentley.com/connect/token)

    The following parameters are used in the request payload using the &quot;application/x-www-form-urlencoded&quot; format:

    - grant\_type=authorization\_code: Tells the token endpoint to use the OAuth 2.0 Authorization Code Flow for this request.
    - code=&lt;authorization\_code&gt;: Provide your one-time use authorization code that you received in step 3.
    - redirect\_uri=&lt;insert\_redirect\_uri\_here&gt;: This is the callback URL that is registered for your application in order to receive the authorization code. The URL must also match the URL that you have provided in the authorization request (see step 1).

    You will then receive the OAuth access token in the server response access\_token field. Note that the expires\_in field in the response represents the validity period of the access token in seconds and it is equal to 3600s.

1. Use the access token to call the API on behalf of the end user

You can now use the access token to call the API as long as it is not expired. Add the provided token to the Authorization header of your API request, using _Bearer_ scheme

---

### Authorization request example

```
https://ims.bentley.com/connect/authorize?response_type=code&client_id=<client_id>&redirect_uri=<redirect_uri>&scope=<scope>&state=<state>
```

### Token request example

```bash
curl https://ims.bentley.com/connect/token -X POST --data-urlencode grant_type=authorization_code --data-urlencode code=<authorization_code> --data-urlencode client_id=<client_id> --data-urlencode client_secret=<client_secret> --data-urlencode redirect_uri=<redirect_uri> --data-urlencode scope=<scope>
```

## AUTHORIZE SINGLE-PAGE APPLICATIONS (SPA) AND DESKTOP/MOBILE APPLICATIONS (NATIVE)

Native and single-page applications are public clients without a dedicated backend server. The implication of this is that these application types cannot securely store a client secret.

- In a native application, the code can be decompiled to reveal the client secret, which is bound to the app and is the same for all users and devices.
- In the case of a single page application, the client secret cannot be stored securely because the entire source is available to the browser.

### Authorization Code Flow with Proof Key for Code Exchange (PKCE)

In order to mitigate issues outlined in [previous section](#authorize-single-page-applications-spa-and-desktopmobile-applications-native), OAuth 2.0 provides an option for Proof Key for Code Exchange (PKCE) by OAuth Public Clients (see OAuth 2.0 [RFC 7636](https://tools.ietf.org/html/rfc7636)). PKCE allows the calling application to dynamically generate a random, one -time key called a &quot;code verifier&quot;. Additionally, the calling app creates a transform of the &quot;code verifier&quot; called the &quot;code challenge&quot; and sends it to the authorization server when obtaining an authorization code. The authorization code obtained is then sent to the token endpoint with the &quot;code verifier &quot;and the server compares it with the previously received request code so that it can perform the proof of the &quot;code verifier&quot; by the client application. This provides a mitigation as the &quot;code verifier&quot; would be unknown to the attacker and cannot be intercepted as it is sent over TLS.

These are the steps for executing the Authorization Code flow with PKCE. Note these steps are very similar to the standard Authorization Code flow with the following additions:

1. Application generates a cryptographically random code\_verifier and from this generates a code\_challenge
1. Redirect the end user&#39;s (resource owner&#39;s) browser to the authorization server endpoint
1. Authenticate the end user and ask for consent
1. The authorization server stores the code_challenge and redirects the end user to your application&#39;s callback URL with an authorization code
1. Exchange the authorization code and the code_verifier for an access token
1. Use the access token to call the API on behalf of the end user

<div class="mermaid">
sequenceDiagram
    participant ro as Resource Owner
    participant app as Application
    participant as as Authorization Server
    participant api as iTwin API

    ro->>+app: Connect to application
    app->>app: Generate code_verifier and code_challenge
    app->>+as: Request authorization code with code_challenge
    as->>ro: Redirect to login and consent
    ro->>as: Sign in and consent
    as->>-app: Authorization code
    app->>+as: Exchange authorization code and code_verifier for an access_token
    as->>as: Validate client_id, code_verifier, code_challenge, scope and redirect_uri
    as->>-app: Granted access token
    app->>-ro: Signed in

    ro->>+app: Perform action
    app->>+api: API request with the access token
    api->>-app: API response
    app->>-ro: Render content

</div>

The following steps outline how to implement the authorization code flow in your application:

1. Application generates a cryptographically random code\_verifier and from this generates a code\_challenge

    This step needs to be completed within your application. There are several libraries available for generating the code\_verifier and code\_challenge.

1. Redirect the end user&#39;s browser to the authorization endpoint

    In order to initiate the end user&#39;s authorization, you must redirect the end user&#39;s browser to Bentley&#39;s authorize endpoint. This will provide a login screen to the end user for authentication. After successful authentication, the consent screen is displayed, if the user has not given the consent yet.

    Authorization endpoint: [https://ims.bentley.com/connect/authorize](https://ims.bentley.com/connect/authorize)

    The URL requires the following parameters:

    - response\_type=code: Request an authorization code as the result of the end user authorization process.
    - code\_challenge=&lt;code\_challenge&gt;: Provide the code generated from the code\_verifier
    - code\_challenge\_method=S256: Provide the method used to generate the challenge, we only support S256.
    - client\_id=&lt;insert\_your\_client\_id\_here&gt;: Provide the client ID of your application.
    - redirect\_uri=&lt;insert\_redirect\_uri\_here&gt;: This is the callback URL that is registered for you application in order to receive the authorization code.
    - scope=&lt;insert\_scopes\_of\_API\_here&gt;: Include the scopes for the API, which are the permissions to request the end users consent for. For each API, you can find the required scopes in the additional API specific documentation. Please note that you will have to request an additional scope &quot;offline_access&quot; to receive a refresh token.
    - state=&lt;insert\_client\_state\_here&gt;: (optional) An opaque value used by the client to maintain state between the request and callback. The authorization server includes this value when redirecting the user-agent back to the client. The parameter SHOULD be used for preventing cross-site request forgery.

1. Authenticate the end user and ask for consent

    This step will be performed by Bentley&#39;s authorization server and does not require anything to be implemented in your application. Redirect the end user to your application&#39;s callback URL with an authorization code

1. The authorization server stores the code_challenge and redirects the end user to your application&#39;s callback URL with an authorization code

    After the end user provides consent for your application, Bentley&#39;s authorization server will store the code_challenge and redirect the end user with an authorization code to the redirect URL registered with your application.

1. Exchange the authorization code for an access token

    After your application has received the authorization code you can exchange it for an access token. The client must authenticate using the HTTP Basic method and provide the clientId (there is no clientSecret as this is a public client) (&lt;insert\_your\_client\_id\_here&gt;:) encoded with BASE64 in the HTTP Authorization header.

    Token Endpoint: [https://ims.bentley.com/connect/token](https://ims.bentley.com/connect/token)

    The following parameters are used in the request payload using the &quot;application/x-www-form-urlencoded&quot; format:

    - grant\_type=authorization\_code: Tells the token endpoint to use the OAuth 2.0 Authorization Code Flow for this request.
    - code=&lt;authorization\_code&gt;: Provide your one-time use authorization code that you received in step 3.
    - redirect\_uri=&lt;insert\_redirect\_uri\_here&gt;: This is the callback URL that is registered for your application in order to receive the authorization code. The URL must also match the URL that you have provided in the authorization request (see step 1). Note: The redirect URL needs to be URL encoded, otherwise an error is thrown.
    - code_verifer: The one-time use code verifier generated by your application in Step 1.

    You will then receive the OAuth access token in the server response. Note that the expires_in field in the response represents the validity period of the access token in seconds and it is equal to 3600s.

1. Use the access token to call the API on behalf of the end user

    You can now use the access token to call the API as long as it is not expired. Add the provided token to the authorization header of your API request.

---

### Authorization request example

```
https://ims.bentley.com/connect/authorize?response_type=code&client_id=<client_id>&redirect_uri=<redirect_uri>&scope=<scope>&state=<state>&code_challenge=<code_challenge>&code_challenge_method=S256
```

### Token request example

```bash
curl https://ims.bentley.com/connect/token -X POST --data-urlencode grant_type=authorization_code --data-urlencode code=<authorization_code> --data-urlencode client_id=<client_id> --data-urlencode redirect_uri=<redirect_uri> --data-urlencode scope=<scope> --data-urlencode code_verifier=<code_verifier>
```

## USING REFRESH TOKENS

To receive a refresh token, you need to request an additional scope &quot;offline_access&quot; in the authorization request. See step 1 in the Authorization Code Flow / Authorization Code Flow with PKCE section for more details of how to pass this scope.

When the offline\_access scope is passed, the response from the authorization server will include both an authorization\_token and a refresh\_token.

When the access token expires, you can use the refresh token in order to obtain a new access token. This way it is not required to request a new authentication/consent from the end user. In addition to the refresh token your client must authenticate using the HTTP Basic method again.

In order to exchange the refresh_token for an access token the following parameters are used in the request payload using the &quot;application/x-www-form-urlencoded&quot; format:

- grant\_type=refresh\_token: This indicates for the token endpoint to refresh an access token for this request. So, it&#39;ll expect a refresh token as part of the parameters.
- refresh\_token=&lt;insert\_your\_refresh\_token\_received\_in\_step\_4\_here&gt;: Provide your one-time token in order to refresh your access token without having to go through the authorization process again.

Our authorization server will give you a new OAuth access token together with a new refresh token.

---

### Token refresh request example

```bash
curl https://ims.bentley.com/connect/token -X POST --data-urlencode grant_type=refresh_token --data-urlencode refresh_token=<refresh_token> --data-urlencode client_id=<client_id> --data-urlencode client_secret=<client_secret> --data-urlencode scope=<scope>
```

## AUTHORIZING SERVICE (MACHINE-TO-MACHINE)

Service apps are designed to operate without user interaction (sometimes called two-legged OAuth) in order to access web-hosted resourced by using the identity of an application. Services run on a server where the source code or configuration of the application is not available to the public. This allows the use of a client secret when communicating with the authorization server to help improve security.

**NOTE:** Your client credentials carry many privileges, so be sure to keep them secure!

- Do not put your client credential information (clientid, client secret or access tokens) in publicly accessible code where they can be discovered.
- Store them in a safe place on the backend (server).

The service app type does not represent any user or organization and does not have access to anything by default. If you want to provide access to projects for that application, you need to invite it to the projects using client email, provided in App details page.

### Client Credential Flow

The Client Credential flow provides the ability for a web service (confidential client) to use it&#39;s own credentials, instead of impersonating a user, to authenticate when calling a web service. Permissions are granted directly to the application itself by an administrator. When the app presents a token to a resource, the resource enforces that the app itself has authorization to perform an action since there is no user involved in the authentication.

These are the steps that the Client Credential flow executes:

1. Redirect the web server to the authorization server endpoint with Client ID and Client Secret
1. Authorization server validates the Client ID and Client Secret and returns Access Token
1. Client uses the access token to call the API

<div class="mermaid">
sequenceDiagram
    participant app as Application
    participant as as Authorization Server
    participant api as iTwin API

    app->>+as: Authenticate using client_id and client_secret
    as->>as: Validate client_id, client_secret and scopes
    as->>-app: Granted access token

    app->>+api: API request with the access token
    api->>-app: API response

</div>

The following steps outline how to implement the authorization code flow in your application:

1. Redirect the web server to the authorization server endpoint with Client ID and Client Secret

    In order to initiate the client credential flow, you need to call Bentley&#39;s token endpoint: [https://ims.bentley.com/connect/token](https://ims.bentley.com/connect/token)

    The URL requires the following parameters:

    - grant\_type=client\_credentials: Must be set to client\_credentials
    - client\_id=&lt;insert\_your\_client\_id\_here&gt;: Provide the client ID of your application.
    - client\_secret=&lt;insert\_your\_client\_secret\_here&gt;: Provide the client secret that was provided when you registered your app. The client secret must be url-encoded before being sent.
    - scope=&lt;insert\_scopes\_of\_API\_here&gt;: Include the scopes for the API, which are the permissions to request the end users consent for. For each API, you can find the required scopes in the additional API specific documentation. Please note that you will have to request an additional scope &quot;offline\_access&quot; to receive a refresh token.

1. Authorization server validates the Client ID and Client Secret and returns Access Token

    This step will be performed by Bentley&#39;s authorization server and does not require anything to be implemented in your application. A successful response will include an access token.

1. App uses the access token to call the API

    You can now use the access token to call the API as long as it is not expired. Add the provided token to the Authorization header of your API request, using _Bearer_ scheme

---

### Token request example

```bash
curl https://ims.bentley.com/connect/token -X POST --data-urlencode grant_type=client_credentials --data-urlencode client_id=<client_id> --data-urlencode client_secret=<client_secret> --data-urlencode scope=<scope>
```

## ERROR RESPONSES

The Authorization Server provides standard HTTP status response codes in the response header.

- A 2xx type response typically represents a successful response.
- A 4xx type response typically represents a client error.
- A 5xx type response typically represents a server error.

The following errors may occur when submitting a request for an access token:

- 400 – Bad request. Common causes include:
  - The given authorization code is not valid or was already used.
  - The redirect\_uri differs from the one registered for your client..
- 401 – Unauthorized. Common causes include:
  - The specified client ID is invalid.
  - The token is not valid (has expired).
- 403 – Forbidden. The client down not have access rights to the resource.
- 429 – Too many requests. The application&#39;s rate limit for the resource has been exhausted.
- 500 – Internal Server Error. This is typically indicative that the endpoint is temporarily unavailable.
- 502 – Bad Gateway. This indicates that the server got an invalid response.

Other OAuth protocol errors can be returned to redirect\_uri in an &quot;error&quot; parameter:

- invalid\_request - The request is missing a required parameter, includes an invalid parameter value, includes a parameter more than once, or is otherwise malformed.
- unauthorized\_client - The client is not authorized to request an authorization code using this method.
- access\_denied - The resource owner or authorization server denied the request.
- unsupported\_response\_type - The authorization server does not support obtaining an authorization code using this method.
- invalid\_scope - The requested scope is invalid, unknown, or malformed.
