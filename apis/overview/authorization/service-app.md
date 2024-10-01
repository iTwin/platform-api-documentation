# Authorize a service application

Service applications are designed to access web-hosted resources without user interaction. They operate using the application's identity and run on a server where the source code or configuration is not publicly available. This setup allows the use of a client secret when communicating with the authorization server. This form of authentication is known as two-legged OAuth, in contrast to three-legged OAuth, which involves user interaction for consent.

The service application type does not represent any user or organization and does not have access to any project data by default. To grant access to projects, you need to invite it using the client email provided on the App Details page after you [register the application](/my-apps/).

## Client Credential Flow

The Client Credential Flow allows your backend process or service, i.e., a confidential client, to authenticate using its own credentials rather than impersonating a user. An administrator grants permissions directly to the application. Since no user is involved in the authentication, the resource enforces that the application is authorized to perform an action when it presents a token to a resource.

The following steps provide an overview of the process.

1. The application makes a request to the authorization server token endpoint with the required parameters.
2. The authorization server confirms the information supplied and returns an access token.
3. The application uses the access token to call a given API.
4. The API responds to the request with the requested data when the necessary scopes are included in the token, and the service identity has the proper permissions for that API.

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

## Set up authorization for your app

The following steps outline how to implement the authorization code flow in your application. Once you have registered [your app](/my-apps), you can begin to obtain the access token.

1. Send a POST request to the authorization server endpoint.

`POST https://ims.bentley.com/connect/token`

The authorization request requires the following parameters:
| **Parameter** | **Description** |
| ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| grant\*type | Set to `client_credentials` for service-based applications. |
| client\*id | The ID of the app you created. If you forgot the ID, find it on the [My Apps](/my-apps/) page. Locate your app in the list. The Client ID is in the same-named column. |
| client*secret | The secret given when you registered the app. If you did not save the client secret, generate a new one. To do so, open the [My Apps](/my-apps/) page and find your app in the list, click the link to open the details page, and then click **Re-generate** in the \_Client Secret* field. |
| scope | Add the `itwin-platform` scope assigned to your app during registration. |

2. The authorization server confirms the `client_id` and `client_secret` and returns an access token. Bentley's authorization server completes this step. There is no implementation needed in your application. A successful response includes the access token.
3. Use the access token to call the API. Remember to call iTwin Platform APIs, you must set up your iTwin roles and permissions. For more information, see the [Access Control API](/apis/access-control/) documentation.

### Token request example

```bash
curl https://ims.bentley.com/connect/token -X POST --data-urlencode grant_type=client_credentials --data-urlencode client_id=<client_id> --data-urlencode client_secret=<client_secret> --data-urlencode scope=<scope>
```
