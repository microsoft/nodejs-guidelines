## Azure and Node.js

### Create a node web app

1. Create your node app locally
2. Navigate to the Azure portal and create a new web app
3. Setup **Continuous Deployment** by navigating to settings and clicking *Continuous Deployment*
4. Select local Git repository
5. Back in settings, select and create your *Deployment credentials*
6. On the **Essentials** header of the web app, note the *Git clone url*
7. Locally, create the git repository by navigating Git Bash to the web app's root directory
8. Run `$ git init`
9. Make your first commit by running `$ git add .` and then `git commit -m "Your commit message"`
10. Add the continuous deployment repository as a remote by running `$ git remote add azure <git_clone_url>`
11. Push your repository to the continuous deployment repository in Azure by running `$ git push azure master`

### Set environment variables in your node web app (CLI)

#### Install the azure CLI package and login (one-time)

1. Install the Azure CLI: `npm install --global azure`
2. Login to your Azure account: `azure login`

#### Set environment variables in your Azure node web app

`azure site appsetting add NEW_ENVIRONMENT_VAR=yourValue your-web-app-name`

*`NEW_ENVIRONMENT_VAR` is the new environment variable name, `yourValue` is the value to set the environment variable to, and `your-web-app-name` is the name of the web app that you intend to set the environment variable for*

#### List environment variables in your Azure node web app

`azure site appsetting list your-web-app-name`.