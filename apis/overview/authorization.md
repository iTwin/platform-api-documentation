<!-- Copyright (c) Bentley Systems, Incorporated. All rights reserved.            -->
<!-- See LICENSE in the project root for license terms and full copyright notice. -->

# Authentication and authorization

## Overview of OAuth

To use Bentley iTwin APIs and SDKs, your application needs the user's consent to access their data. We use OAuth 2.0 to grant access. Follow these steps to set up OAuth 2.0 for your application. For detailed specifications, see [rfc6749](https://tools.ietf.org/html/rfc6749).

Before starting the OAuth process, you must register your app with the iTwin Platform. During registration, provide basic information such as the app name and redirect URI, which redirects users to the appropriate web server, browser, or native app. If you haven't registered your application, visit the [My Apps](/register) page to register your application.

To open the _My Apps_ page, click your **Profile** button in the upper right corner and then **My Apps**. You must be logged in to see the **Profile** button.

**Note:** Service applications without user interaction do not require a redirect URI. Instead, they authenticate using a _client secret_ provided at the end of the registration process. The automatically created user identity for the Service application needs a role assigned to make requests to the iTwin Platform. This is done using the [Access Control API](/apis/access-control/). For more information on setting up your service application, see the [Authorizing a Service App](/tutorials/authorize-service/) guide.

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

## Application scopes and user permissions

The iTwin Platform uses a universal `itwin-platform` scope that allows applications to access all APIs without the need to have individual scope associations. This scope is included as part of the OAuth process to retrieve an access token. For more information, see [introduction of itwin-platform scope](/itwin-platform-scope-introduction/).

Data associated with your iTwin is kept secure through user permissions using the Access Control API. This API uses Role-based Access Control (RBAC) to determine the permissions available to end users of your application. See the example below.

**Example:**

You create an application named **My App** with the `itwin-platform` scope. You have a user, **User A**, that wants to create an iTwin through your application. **User A** must have a role with the `itwins_create` permission to create the iTwin within your application.  While the application has the ability to create iTwins as part of the `itwin-platform` scope, the end user does not have the appropriate permissions in the role they are assigned, `itwins_create`. See the [Access Control API](/apis/access-control/) documentation for information on setting up end-user permissions.

## Authorizing your applications

The method of retrieving your access token depends on OAuth 2.0 flow. The authorization flow of your application depends on your application type as well as the ability to keep client secrets secure. The following sections describe the different types of applications and their authorization methods.

### Authorize a service application

A service application typically runs in the background or on a server, providing data or services to other applications. For example, in the iTwin Platform, such an application could automatically sync and update an iTwin's design data to reflect latest information. For authorization documentation, see [Authorize a service application](/apis/overview/authorization/service-app/). For a tutorial, see [Authorize a service application tutorial](/tutorials/authorize-service/).

### Authorize a web application

An application built on a server-side framework, accessed through a web browser over a network. For authorization documentation, see [Authorize a web application](/apis/overview/authorization/web-app/). For a tutorial, see [Authorize a web application tutorial](/tutorials/authorize-webapp/)

### Authorize a native application

An application designed to run natively on a specific operating system or device, providing optimal performance and integration with system features. For authorization documentation, see [Authorize a native or SPA application](/apis/overview/authorization/native-spa/). For a tutorial, see [Authorize a native application tutorial](/tutorials/authorize-native/).

### Authorize a single-page application (SPA)

A web application that loads a single HTML page and dynamically updates the content as the user interacts with the app, enhancing user experience by avoiding full page reloads. For authorization documentation, see [Authorize a native or SPA application](/apis/overview/authorization/native-spa/). For a tutorial, see [Authorize a single-page application (SPA) tutorial](/tutorials/authorize-spa/).

## Refresh tokens

Access tokens have an expiry time. In the iTwin Platform, access tokens expire after 3600 seconds, before which a client needs to request a refresh of the token. Requesting refresh tokens is possible in web and native (desktop/mobile) applications. When requesting a refresh token, you must include the `offline_access` scope as part of the authorization request. This scope is added to the request as you would add any other scope in an OAuth request. Tokens are _Bearer_ type, which must be specified in your API calls.

Token endpoint: `POST https://ims.bentley.com/connect/token`

Request parameters:

| Field Name    | Description                                                                                                                                           |
| ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| client_id     | Identification generated during application creation. Found in the [My Apps](/my-apps) page or in the first step if generated during the tutorial.    |
| client_secret | Secret created during application creation. Only required for a web application.                                                                      |
| grant_type    | Set to `refresh_token` Indicates the type of grant being used. This tells the service you are requesting a new `access_token` with a `refresh_token`. |
| refresh_token | The refresh token. Ensure the `refresh_token` you include is the same one received from the previous request.                                         |
