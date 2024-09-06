# Visualization

## iTwin Viewer

The iTwin Viewer is a configurable iTwin.js viewer that provides the ability to view and interact with iModels. It includes basic capabilities and can be extended with iTwin.js extensions. The iTwin Viewer includes several tools.

- Selection tools to select, hide, and emphasize elements
- Basic measurement tools
- Basic clipping tools
- Basic navigation tools to pan, zoom, and rotate
- Walk tool and camera tool
- Basic tree view and property grid
- Status bar with tool-specific contextual information

## Creating an app to view an iModel

You can use <a href="https://create-react-app.dev/" target="_blank">Create React App</a> to quickly set up a single page React application to view an iModel. The <a href="https://www.npmjs.com/package/@itwin/cra-template-web-viewer" target="_blank">iTwin Viewer Create React App Template</a> provides a template for Create React App for applications which are based on the iTwin Viewer. The following steps can be used to develop and build the application.

### Development prerequisites

First you need to install the required prerequisites. Writing an iTwin.js application requires <a href="https://nodejs.org" target="_blank">Node.js</a> (LTS version) which provides the backend JavaScript runtime. The installation also includes the `npm` command line tool.

### Suggested tools

- <a href="https://code.visualstudio.com/" target="_blank">Visual Studio Code</a> is the recommended editor and debugger for iTwin.js applications. VS Code also supplies a graphical user interface for working with Git.
- <a href="https://www.google.com/chrome/" target="_blank">Google Chrome</a> is the preferred tool for developing and debugging frontend JavaScript.
- The VS Code extension <a href="https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-chrome" target="_blank">Debugger for Chrome</a> can also be quite helpful.

### Recommended reading

- <a href="https://www.typescriptlang.org/" target="_blank">TypeScript</a>

  iTwin.js applications are written in TypeScript and then _compiled_ to plain JavaScript.

- <a href="https://www.npmjs.com/" target="_blank">Node Package Manager (npm)</a>

  `npm` is used to install and manage dependencies of an iTwin.js application. The `npm` <a href="https://docs.npmjs.com/cli/npm" target="_blank">command line</a> and `npm` <a href="https://docs.npmjs.com/misc/scripts" target="_blank">scripts</a> are used to build and test iTwin.js applications.

### Development steps

1. Install the necessary prerequisites.
2. From a terminal, `npx create-react-app@latest your-app-name --template @itwin/web-viewer --scripts-version @bentley/react-scripts`.

   This will generate a new application based on the iTwin Viewer React component in the `your-app-name` directory.

3. Open the `your-app-name` directory in VS Code.
4. Go to https://developer.bentley.com in a web browser.
5. Click the **Sign In** button and sign-in using your Bentley account credentials
   - If you have not already registered, click **Register now** and complete the registration process.
6. Click on your user icon and navigate to the **My Apps** page
7. Click the **Register New** button
8. Give your application a Name
9. Select the **Visualization** API
10. Select application type **SPA** (Single Page Web Application)
11. Enter **Redirect URL** `https://localhost:3000/signin-callback`
12. Leave post logout redirect URIs empty.
13. Click the **Save** button
14. Once your new application is saved and a clientId is generated, add the clientId, list of scopes, and redirect url to the following variables in the .env file within the application's root directory: `IMJS_AUTH_CLIENT_CLIENT_ID`, `IMJS_AUTH_CLIENT_SCOPES`,`IMJS_AUTH_CLIENT_REDIRECT_URI`.
15. Add a valid iTwinId and iModelId for your user to the `IMJS_ITWIN_ID` and `IMJS_IMODEL_ID` variables in the same .env file. You can obtain the ids using the iTwins and iModels REST APIs.
16. From a terminal at your application's root directory, `npm start`. This will serve the application with live reloading.
17. Add/Update/Remove files as needed for your use case. If running `npm start` while making changes, your application should re-compile and reload.
18. The viewer can be modified via the Viewer component in the App.tsx file. Visit the <a href="https://www.npmjs.com/package/@itwin/web-viewer-react" target="_blank">iTwin Viewer React</a> documentation for more information.
19. Review the <a href="https://github.com/iTwin/viewer/blob/master/packages/templates/cra-template-web-viewer/README.md" target="_blank">README.md</a> file in the root directory of your application for additional development information.

### Build

From a terminal at your application's root directory, `npm run build`. This will create a deployment-ready build in the "build" folder within the application's root directory. It is not necessary to build the application during development.

### References

- <a href="https://create-react-app.dev/" target="_blank">Create React App</a>
- <a href="https://www.npmjs.com/package/@itwin/web-viewer-react" target="_blank">iTwin Viewer React</a>
- <a href="https://www.npmjs.com/package/@itwin/cra-template-web-viewer" target="_blank">iTwin Viewer Create React App Template</a>
- <a href="https://www.npmjs.com/package/@bentley/react-scripts" target="_blank">Bentley React Scripts</a>

## Extending the capabilities

The iTwin Viewer can be extended with iTwin.js extensions. An iTwin.js extension is a separate JavaScript module that can load on demand into an iTwin.js frontend application. The separate deliverable enables an extension to provide extensibility of an iTwin.js application at runtime.

Each extension is its own separate bundle that has access to all iTwin.js shared libraries to enable seamless integration with the host app. Extensions can be used to expand the behavior of iTwin Viewer to support your custom workflows. The iTwin.js SDK includes more information about creating <a href="https://www.itwinjs.org/learning/frontend/extensions/" target="_blank">iTwin.js extensions</a>.
