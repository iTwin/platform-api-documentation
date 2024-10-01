# Authorize a native or single-page application (SPA)

Desktop/mobile (native) and single-page applications (SPAs) are public and lack a dedicated backend server for storing a client secret securely. Instead, these applications use Proof Key for Code Exchange (PKCE) to ensure secure access to protected resources.

- In a native application, the code can be decompiled to reveal the client secret, which is bound to the app and is the same for all users and devices.
- In the case of a single page application, the client secret cannot be stored securely because the entire source is available to the browser.

## Authorization code flow with Proof Key for Code Exchange (PKCE)

Native applications and SPAs can use the OAuth 2.0 Authorization Code Flow to enable data owners to authorize third-party apps to access user data. However, as opposed to [web apps](/tutorials/authorize-webapp), these applications cannot keep a client secret as the entire source is accessible to the public. In order to mitigate this, OAuth 2.0 provides an option for Proof Key for Code Exchange (PKCE) by OAuth Public Clients (see OAuth 2.0 [RFC 7636](https://tools.ietf.org/html/rfc7636)) to securely obtain an authorization code. PKCE allows the calling application to dynamically generate a random, one-time key called a &quot;code verifier&quot; to accomplish this.

Additionally, the calling app creates a transform of the &quot;code verifier&quot; called the &quot;code challenge&quot; and sends it to the authorization server when obtaining an authorization code. The authorization code obtained is then sent to the token endpoint with the code verifier and the server compares it with the previously received request code so that it can perform the proof of the code verifier by the client application. This provides a mitigation as the code verifier would be unknown to the attacker and cannot be intercepted as it is sent over TLS.

The following steps provide an overview of this process.

1. The application generates a cryptographically random `code_verifier` and from this generates a `code_challenge`.
2. The application makes a request to the authorization server endpoint.
3. The end-user provides their authentication information and consents for the application to access resources on their behalf.
4. The authorization server stores the `code_challenge` and returns an authorization code to the Redirect URI specified when creating the application.
5. The application uses the authorization code and `code_verifier` to obtain an access token from the authorization server.
6. The application uses the access token to call the API on behalf of the user.

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

## Set up authorization for your app

The following steps outline how to implement the authorization code flow in your application. Once you have registered [your app](/my-apps), you can begin to obtain the access token.

1. Generate `code_verifier` and `code_challenge`. This step needs to be completed within your application. There are several libraries available for generating the `code_verifier` and `code_challenge`.

2. When the user opens the application, redirect them to the authorization server endpoint. This will provide a login screen to the end user for authentication. After successful authentication, the consent screen is displayed, if the user has not given the consent yet.

   Authorization endpoint: `https://ims.bentley.com/connect/authorize`

   The request for an authorization code requires the following parameters:

   | Parameter               | Description                                                  |
   | ----------------------- | ------------------------------------------------------------ |
   | response_type           | Set to `code` to indicate that an authorization code is needed. |
   | client_id               | The ID of the app you created. If you forgot the ID, find it on the [My Apps](/my-apps) page. Locate your app in the list, and the Client ID is in the same-named column. |
   | redirect_uri            | The callback URL you entered when registering your application. The returned authorization code is sent to this URL. In this case, the callback URL must be `https://developer.bentley.com/redirect-tutorial`. |
   | scope                   | Add the `itwin-platform` scope assigned to your app during registration. When requesting a refresh token, include the scope `offline_access`. Separate multiple scopes with a space. Your end user will consent to the app accessing this information on their behalf during the login process. |
   | code_challenge          | The code generated from the `code_verifier`. You can copy the `code_challenge` from step 1. |
   | code\_challenge\_method | The method used to generate the challenge, we only support S256. |
   | state                   | (Optional) Used by the client to maintain state between a request and a callback. Recommended to prevent cross-site request forgery. The authorization server includes this value when redirecting the user-agent to the client. |

3. The user signs in to authenticate and consents for the application to access resources on their behalf. This page is managed by the Bentley authorization server and does not require any implementation in your application.

   ![User interface for facing Bentley authorization server](/images/tutorials/authorize-webapp/user-signin-consent.png)

   Once authenticated, the Bentley authorization server stores the code_challenge and returns an authorization code to the Redirect URI registered with your application. Extract the `code` in the response from the `redirect_uri`.

   `https://example-rediect-uri?code=<code>`

   **NOTE:** Authorization codes are time-sensitive. If your code expires, send a new request to the authorization server for a new code.

4. Send a request to the token endpoint to exchange the authorization code for an access token.

   `POST https://ims.bentley.com/connect/token`

   The authorization request requires the following parameters:

   | Field Name    | Description                                                                                                                                        |
   | ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
   | client_id     | Identification generated during application creation. Found in the [My Apps](/my-apps) page or in the first step if generated during the tutorial. |
   | grant_type    | Set to `authorization_code` Indicates the type of grant being used. This tells the service you are exchanging the code for a token.                |
   | code_verifier | The one-time-use code verifier generated by your Application.                                                                                      |
   | code          | This is the authorization code returned in the previous request.                                                                                   |
   | redirect_uri  | The callback URL you entered when registering your application. This URL must match the URL provided in the initial request.                       |

5. The authorization server confirms the information sent in the request and returns an access token. Bentley's authorization server completes this step. There is no implementation needed in your application.
   A successful response includes the `access_token`, an expiry of 3600 seconds, and a `refresh_token`. Tokens are _Bearer_ type, which must be specified in your API calls.

6. Use the access token to call the API. Tokens are added to the `Authorization` header with `Bearer` type in subsequent requests. Successfully sending a request to an API requires the end user to have the correct account permissions. Use the [Access Control API](/apis/access-control/) to ensure your user can access the required resources.

---

### Authorization request example

```
https://ims.bentley.com/connect/authorize?response_type=code&client_id=<client_id>&redirect_uri=<redirect_uri>&scope=<scope>&state=<state>&code_challenge=<code_challenge>&code_challenge_method=S256
```

### Token request example

```bash
curl https://ims.bentley.com/connect/token -X POST --data-urlencode grant_type=authorization_code --data-urlencode code=<authorization_code> --data-urlencode client_id=<client_id> --data-urlencode redirect_uri=<redirect_uri> --data-urlencode scope=<scope> --data-urlencode code_verifier=<code_verifier>
```
