# **Deploying a React App**

In this section we will get to deploying our static assets and posting our React App to the web.

We can deploy our application using services like GitHub pages, Netlify or Vercel but in this section we will use Netlify because it is extreamly simple to deploy an app to the Netlify using GitHub.

## **Create Production Build**

To create the production build we simplt need to pass this command to out terminal window.

```npm
npm run build
```

Now that command should build for us a new folder that we should deploy.

To serve our build we need to first install serve package globally.

```npm
npm i -g serve
```

Once we do that we can run this

```npm
serve -s build
```

We can now check if this build was serced by typing in the browser localhost:5000

Now we can deploy that build to any host we want.

As I mentioned earlier we will use Netlify with GitHub.

All we have to do is to upload page via GitHub and make sure that build directory is selected.
