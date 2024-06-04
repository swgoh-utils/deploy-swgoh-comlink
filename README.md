# Deploy SWGOH Comlink to a hosting service

This repo is used to create a quick and easy way to deploy and update SWGOH Comlink using GitHub.

Visit the main [SWGOH Comlink repo](https://github.com/swgoh-utils/swgoh-comlink) to learn more about what SWGOH Comlink is and how to use it.

### Free Hosting limitations

If you are looking to use a free hosting service to run Comlink be sure to carefully read through any limitations they may have. Most will be limited on how much data it can deliver at one time. This means you may have to _request the localization file in zip format_ from the `/localization` endpoint and you may have to request information from the `/data` endpoint _in segments_, prefereably with `includePveUnits` set to false.

Check out [Discord](https://discord.gg/Kwnrfwu2NP) for a list of free hosting providers that work decent with Comlink.

### Comlink limitations

In order to calculate stats for player rosters you must use the roster data with [SWGOH Stats](https://github.com/swgoh-utils/swgoh-stats) which may need to be hosted on a separate account if you are using free hosting. You can use the following repo to quickly set it up: [swgoh-utils/deploy-swgoh-stats](https://github.com/swgoh-utils/deploy-swgoh-stats).

\_

## GENERAL DEPLOY STEPS USING GITHUB

#### 1. Create a GitHub account.

#### 2. Create a new private repository and copy the files from this repo into it.

If you Fork this repo it will remain public and others can see the app you have delpoyed it to. It is recommended that you copy these files to a private repo to keep others from using your service hours/resources.

#### 3. Create an account on the hosting service if you have not already and then navigate in their dashboard to where you can add a new application/dyno/service. Make sure to select Web Service for the application type.

#### 4. Choose to add the applictaion from Github, it could also be stated as Connect with Github. It is recommended to only give it access to specific repositories and to auto-deploy new updates when prompted. Some hosting providers may require you to do manual deploys for updates.

#### 5. Select your private fork of this repo. It should start the install automatically. After the install it will most likely fail starting up due to required Environment Variables.

#### 6. Navigate to the settings in that application that deal with environment variables. This could be stated as Reveal Config Vars, Configure Environment Variables, etc...

##### Environment variables:

| Variable Name | Description        | Notes                 |
| ------------- | ------------------ | --------------------- |
| `APP_NAME`    | your app name      | Required              |
| `ACCESS_KEY`  | your "public" key  | Optional, Recommended |
| `SECRET_KEY`  | your "private" key | Optional, Recommended |

Setting an access key and secret key will keep unauthorized users from using your app.

#### 7. Once you have set the environment variables restart the application and verify in the logs that it started successfully. It should say SWGOH-Comlink is listening on port xxxx in the log.

\_

## GENERAL DEPLOY STEPS USING DOCKER
1. Create an account on the hosting service if you have not already and then navigate in their dashboard to where you can add a new application/dyno/service. Make sure to select Web Service for the application type.

2. Choose to add the applictaion from an existing registry. The option should say or mention Docker or Docker Hub somewhere in it.

3. For the image URL use the following: ***ghcr.io/swgoh-utils/swgoh-comlink:latest***

4. Follow the steps for selecting a name for your dyno, select the appropriate price tier you want to use, and then enter the above mentioned Environment Variables.


## START UP HELP BY HOSTING PROVIDER
### Render
1. After setting up an account go to your dashboard and select New then select Web Service

2. Click Build and deploy from a Github repository then follow above steps for copying this repo from the General deploy steps. Alternatively you can select the Deploy an existing image from a registry and then entering the image URL from the General Deploy Steps Using Docker option.

### Northflank
1. After setting up an account, choose to set up a new Web Service and select the Docker option.

2. Follow the General Deploy Steps Using Docker above.

### Railway (railway.app)

1. Download a copy of the files in this repository to your local machine; unzip the download and grab the `Dockerfile` and the `app.json` file (For simplicity, you can discard the README and heroku.yml files if you like.)

2. Create a new private GitHub repository, and upload the `Dockerfile` and `app.json` files you downloaded.

3. In the Railway Dashboard, create a new Project (with whatever name you choose) and enter the project.

4. Inside the project, click the `+ New` button in the top right, and select `GitHub Repo` --> `Configure GitHub App`, and log into your GitHub account

5. Under `Repository Access`, select `Only select repositories`, then use the dropdown to select the comlink repository you created. Click the green `Save` button and exit the pop up window.

6. In your Railway project, click `+ New` again, then `GitHub Repo`, then the name of the repository you created. A new deployment with a random name will appear in the Project window.

7. Once the deployment shows a green check mark, click the deployment to enter the settings window. In the `Deployments` tab, click the `View Logs` button on the right side. If the build was successful, you'll see the following message in the Deploy Logs window:

> You must either specify your application name via the argument --name, or with the environment variable APP_NAME. See --help for more details.

8. Move to the `Settings` tab and under `Environment` --> `Domains`, click the `Generate Domain` button. A new URL ending in `.up.railway.app` will appear. _Save this address for later! This is the URL you will send requests to to access comlink data._

9. Move to the `Variables` tab and click the `+ Add Variable` button in the top right. Set the new variable name as `APP_NAME` and its value as whatever name you like. Exit the settings window, which will cause the app to restart.

10. When you see the green check mark, navigate back to the Deploy Log. Once comlink is running, you should see a version of the following message in the log:

> swgoh-comlink:1.11.0 is listening on port 1234 with app name 'rutabaga!'

11. Enjoy your new Comlink!

**NOTE**: When you send requests to comlink, you will _not need to provide a port number_. Railway automatically maps the URL you generated to the port your comlink instance is listening on!
