# iTwin.js Extensions API

The iTwin.js Extensions API provides a method to create, upload and retrieve extensions which can be loaded into iTwin.js applications.

## Extensions

An iTwin.js Extension is a separate module that can be loaded on demand into an iTwin.js application.

### Use cases

Extensions can be used for many different purposes, such as:

- Add a new [view decorator](https://www.itwinjs.org/learning/frontend/viewdecorations/) to an existing frontend application to better support your custom workflows.
- Write event based processing, i.e., subscribe to an iModel Event, or Unified Selection Event, and process that change.

### Authorization

You can view and download extensions created within their organization without needing any new roles assigned. If you wish to create and upload extensions, you need the Manage Extensions permission. Please contact your organization's administrator for permission.

> If you have access to a single iTwin inside an organization, you also have access to all that organization's extensions even if you are not in the organization yourself.

To learn more, see [Roles and Permissions](https://developer.bentley.com/roles-and-permissions/).

## Workflow
<!-- Maybe add a diagram? -->
A typical workflow involves the following:

1. Create a private extension associated with an Account iTwin.
2. Create a new version for the extension.
3. Upload the JavaScript module associated with the version.
4. Get the extension, including the version of it you would like.
5. Load the extension into your iTwin application.

### Steps

#### 1. Create a private extension associated with an iTwinId

Start off by [creating a new private extension](https://developer.bentley.com/apis/extensions/operations/create-private-extension/), providing a name, an Account iTwinId, and an optional description. The iTwin must be of class `Account` - creating an extension under a project iTwin is not allowed. See [Account iTwins](https://developer.bentley.com/apis/itwins/overview/#account) for more details.

#### 2. Create a new version for the extension

Using the extension Id received from the response body in step 1, [create a new version of the extension](https://developer.bentley.com/apis/extensions/operations/create-extension-version/).
> The version number passed into the PUT request must match the `version` found in your extension's `package.json`. All version numbers should follow [semantic versioning rules](https://semver.org/).

#### 3. Upload the JavaScript module associated with the version

Using a PUT request, upload an archived folder of your extension through the upload URL received from the response body in the previous step.
> To clarify, the archived folder's file type must be zip, tarball, or gzip.

**Package.json requirements**:

1. `name` field must match the name of your extension.
2. `version` field must match semantic version you provided when creating a new version of your extension.
3. `main` field contains path to a JavaScript entry file.
4. Has a dependency or peer dependency to the `@itwin/core-extension` package.

After successfully uploading your extension, other users who can view the extension will be able to use them.
> At the moment, we do not provide delete functionality. If publishing of extension version failed, you may need to bump extension version in manifest file, and create a new extension version before trying again.

#### 4. Get the extension, including the version of it you would like

After uploading, you can check the status of the archive extraction through [Get Private Extension Version](https://developer.bentley.com/apis/extensions/operations/get-private-extension-version/). Once extraction is complete, the endpoint will also return the files that make up the extension.

Alternatively, you can use [Get Latest Extension Version](https://developer.bentley.com/apis/extensions/operations/get-latest-extension-version/) to get the most recent version that is available for download. If the extension has no versions ready, it will return a status code of 404.

If you have multiple different extensions saved to your iTwin organization, you can use the [Get Private Extensions](https://developer.bentley.com/apis/extensions/operations/get-private-extensions/) endpoint to see the list of extensions available.

#### 5. Load the extension into your iTwin application

You can load an extension into an iTwin.js application using the [@itwin/extension-client](https://www.npmjs.com/package/@itwin/extension-client) package.

<!-- TODO: Update this section with applications that consume extensions (iTwin Studio + Pineapple) and how they load it. Maybe a link to their docs in the future to update them? -->

## Learning

For more information, see [iTwin.js Extensions](https://www.itwinjs.org/learning/frontend/extensions/).
