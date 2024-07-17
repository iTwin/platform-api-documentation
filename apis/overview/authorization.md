<!-- Copyright (c) Bentley Systems, Incorporated. All rights reserved.            -->
<!-- See LICENSE in the project root for license terms and full copyright notice. -->

# Authentication and Authorization

## Overview of OAuth

To use Bentley iTwin APIs and SDKs, your application needs the user's consent to access their data. We use OAuth 2.0 to grant access. Follow these steps to set up OAuth 2.0 for your application. For detailed specifications, see [rfc6749](https://tools.ietf.org/html/rfc6749).

Before starting the OAuth process, you must register your app with the iTwin Platform. During registration, provide basic information such as the app name and redirect URI, which redirects users to the appropriate web server, browser, or native app. If you haven't registered your application, visit the [My Apps](https://developer.bentley.com/register) page to register your application.

To open the _My Apps_ page, click your **Profile** button in the upper right corner and then **My Apps**. You must be logged in to see the **Profile** button.

**Note:** Service applications without user interaction do not require a redirect URI. Instead, they authenticate using a _client secret_ provided at the end of the registration process. The automatically created user identity for the Service application needs a role assigned to make requests to the iTwin Platform. This is done using the [Access Control API](https://developer.bentley.com/apis/access-control/). For more information on setting up your service application, see the [Authorizing a Service App](https://developer.bentley.com/tutorials/authorize-service/) guide.

## Key terminology

| **Term**                 | **Description**                                                                                                                                                                                                                                                                            |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Access Token**         | A string that allows authorized access to protected resources within an API. It has a limited lifetime, specified scopes, and may include other information required by the server.                                                                                                        |
| **Authorization Server** | Verifies the user's identity and application credentials and generates access tokens for the app. These tokens enable the app to access protected resources on behalf of the user.                                                                                                         |
| **Client**               | An application that accesses protected resources on behalf of the resource owner (i.e., the end user). It can be hosted on a server, desktop, or mobile device.                                                                                                                            |
| **Client ID**            | A unique public identifier for an app.                                                                                                                                                                                                                                                     |
| **Client Secret**        | A random string that is known only to the application and authorization server. This string is required for authorizing confidential clients to prevent the authorization server from providing tokens to unauthorized apps                                                                |
| **Confidential Client**  | Clients that can maintain the confidentiality of the Client Secret, typically running on a server under the developer’s control, where the source code and configuration are not accessible to users                                                                                       |
| **Public Client**        | Clients that cannot maintain the confidentiality of a Client Secret, such as mobile, desktop, and browser apps. A client secret should not be used in these apps because other developers can easily discover it, compromising the security of your application and data.                  |
| **Redirect URI**         | Used by the authorization server to send the user back to the application with an authorization code after the user has successfully authorized the app.                                                                                                                                   |
| **Refresh Token**        | A string that enables the retrieval of a new access token once the current access token has expired. This token is required for making authorized requests on behalf of the user that do not require user interaction, such as background jobs or long-running tasks.                      |
| **Scope**                | OAuth 2.0 scopes restrict the access granted to an access token, determining which protected resources can be accessed and the level of access granted (e.g. READ or WRITE). To avoid a 401 Unauthorized response, a client must include the required scopes when calling an API endpoint. |

## Application Scopes and User Permissions

The iTwin Platform uses a universal `itwin-platform` scope that allows applications to access all APIs without the need to have individual scope associations. This scope is included as part of the OAuth process to retrieve an access token. For more information, see [introduction of itwin-platform scope](https://developer.bentley.com/itwin-platform-scope-introduction/).

Data associated with your iTwin is kept secure through user permissions using the Access Control API. This API uses Role-based Access Control (RBAC) to determine the permissions available to end users of your application. See the example below.

**Example:**

You create an application named **My App** with the `itwin-platform` scope. You have a user, **User A**, that wants to create an iTwin through your application. **User A** must have a role with the itwins_create permission to create the iTwin within your application.  While the application has the ability to create iTwins as part of the `itwin-platform` scope, the end user does not have the appropriate permissions in the role they are assigned, itwins\_create. See the [Access Control API](https://developer.bentley.com/apis/access-control/) documentation for information on setting up end-user permissions.

## Authorizing your applications

The method of retrieving your access token depends on OAuth 2.0 flow. The authorization flow of your application depends on your application type as well as the ability to keep client secrets secure. The following sections describe the different types of applications and their authorization methods. Click the heading link for detailed instructions for each type of application.

### [Authorize a service application](https://developer.bentley.com/tutorials/authorize-service/)

Service applications, also known as two-legged authorization, are designed to access web-hosted resources without user interaction. They operate using the application's identity and run on a server where the source code or configuration is not publicly available. This allows for using a client secret when communicating with the authorization server.

### [Authorize a web application](https://developer.bentley.com/tutorials/authorize-webapp/)

Web applications are built using a server-side framework, which runs on a private server to secure communication with the authorization server. This ensures that the application's source code or configuration remains inaccessible to the public and allows for using a client secret.

### [Authorize a Desktop/Mobile application](https://developer.bentley.com/tutorials/authorize-native/)

For desktop and mobile applications that do not have a dedicated backend server and are public, making it impossible to store a client secret securely. Instead, these applications use Proof Key for Code Exchange (PKCE) to ensure secure access to protected resources.

### [Authorize a Single Page Application (SPA)](https://developer.bentley.com/tutorials/authorize-spa/)

Single Page Applications (SPAs) that are public and lack a dedicated backend server cannot store a client secret securely. To address this, SPAs use Proof Key for Code Exchange (PKCE) to ensure secure access to protected resources.

## Refresh Tokens

Access tokens contain an expiry time. In the iTwin Platform, access tokens expire after 3600 seconds, before which you need to request a refresh of the token. When requesting a refresh token, you must include the _offline_access_ scope as part of the authorization request. This scope is added to the request as you would add any other scope in an OAuth request.
