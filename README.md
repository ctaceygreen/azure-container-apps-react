# Azure Container Apps React
This repo shows a simple example of how to host a default React App on ACA. Azure Container Apps is a great serverless container option within Azure, and the simplicity of this repo should be evidence of that.

If you have an app that runs in a container locally, throwing it into ACA is going to be incredibly simple!

# So how does this all fit together?
- There's the React App itself in the src folder, which was bootstrapped with [Create React App](https://github.com/facebook/create-react-app). (See default README below)
- There are two Dockerfiles. One for running a development version of the app locally (Dockerfile.dev) and the other to use when deploying to production (Dockerfile)
    - These are no different from what you'd expect when hosting a React app on any containerised environment (Kubernetes etc)
- Great, so now we need to deploy this app somewhere. The .azuredevops folder contains everything you'll need for our Azure DevOps pipeline. Spoilers: It's very basic.
    - Our pipeline does two main things...
        - Build and push a Docker image of our application to a container registry
            - In this example, I've chosen to use DockerHub as our registry. This is purely to be cheap. If I were deploying an enterprise application, I'd be looking to use Azure Container Registry or similar.
        - Deploy the Infrastructure of an Azure Container App (along with a few other things), pointing to our lovely Docker image
- The final piece of the puzzle lives within our 'infra' folder. Here we have our Bicep IaC, defining a Container App, a Container Apps Environment, and a Log Analytics Workspace.

# How can I get this up and running within my own ?
You'll need to setup a few things first, and then it's just a case of replacing some variables :)
1. Create a DockerHub account (if you want to use a different registry that's absolutely fine too. You'll just need to change the 'registryServer' parameter within the IaC)
2. Create the usual foundations in Azure (if you need help creating these, there are many other useful resources out there to show you how!):
    - Subscription
    - Resource Group
    - Service Connection (Azure Resource Manager)
    - Service Connection (Docker Registry)
3. Create an Azure DevOps pipeline, and point it at the file '.azuredevops/azure-pipelines.yml'
4. The variables for your pipeline all live within '.azuredevops/variables'. This is where you'll need to replace all instances of "<REPLACEME>" with your own values.
5. Run your pipeline from ADO, and get many green ticks of instant gratification :D

# So let's look into the interesting parts of this repo in a bit more detail...
TODO

# Getting Started with Create React App

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in your browser.

The page will reload when you make changes.\
You may also see any lint errors in the console.

### `npm test`

Launches the test runner in the interactive watch mode.\
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `npm run build`

Builds the app for production to the `build` folder.\
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.\
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `npm run eject`

**Note: this is a one-way operation. Once you `eject`, you can't go back!**

If you aren't satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you're on your own.

You don't have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn't feel obligated to use this feature. However we understand that this tool wouldn't be useful if you couldn't customize it when you are ready for it.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).

### Code Splitting

This section has moved here: [https://facebook.github.io/create-react-app/docs/code-splitting](https://facebook.github.io/create-react-app/docs/code-splitting)

### Analyzing the Bundle Size

This section has moved here: [https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size](https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size)

### Making a Progressive Web App

This section has moved here: [https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app](https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app)

### Advanced Configuration

This section has moved here: [https://facebook.github.io/create-react-app/docs/advanced-configuration](https://facebook.github.io/create-react-app/docs/advanced-configuration)

### Deployment

This section has moved here: [https://facebook.github.io/create-react-app/docs/deployment](https://facebook.github.io/create-react-app/docs/deployment)

### `npm run build` fails to minify

This section has moved here: [https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify](https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify)
