# Deploy SWGOH Comlink to a hosting service
This repo is used to create a quick and easy way to deploy and update SWGOH Comlink using GitHub.

Visit the main [SWGOH Comlink repo](https://github.com/swgoh-utils/swgoh-comlink) to learn more about what SWGOH Comlink is and how to use it.

### Free Hosting limitations
If you are looking to use a free hosting service to run Comlink be sure to carefully read through any limitations they may have. Most will be limited on how much data it can deliver at one time. This means you may have to _request the localization file in zip format_ from the `/localization` endpoint and you may have to request information from the `/data` endpoint _in segments_, prefereably with `includePveUnits` set to false.

Check out [Discord](https://discord.gg/Kwnrfwu2NP) for a list of free hosting providers that work decent with Comlink.

### Comlink limitations
In order to calculate stats for player rosters you must use the roster data with [SWGOH Stats](https://github.com/swgoh-utils/swgoh-stats) which may need to be hosted on a separate account if you are using free hosting. You can use the following repo to quickly set it up: [swgoh-utils/heroku-swgoh-stats](https://github.com/swgoh-utils/heroku-swgoh-stats).

_
## GENERAL DEPLOY STEPS
#### 1. Create a GitHub account.

#### 2. Create a new private repository and copy the files from this repo into it.
If you Fork this repo it will remain public and others can see the app you have delpoyed it to. It is recommended that you copy these files to a private repo to keep others from using your service hours/resources.

#### 3. Create an account on the hosting service if you have not already and then navigate in their dashboard to where you can add a new application/dyno/service. Make sure to select Web Service for the application type.

#### 4. Choose to add the applictaion from Github, it could also be stated as Connect with Github. It is recommended to only give it access to specific repositories and to auto-deploy new updates when prompted. Some hosting providers may require you to do manual deploys for updates.

#### 5. Select your private fork of this repo. It should start the install automatically. After the install it will most likely fail starting up due to required Environment Variables.

#### 6. Navigate to the settings in that application that deal with environment variables. This could be stated as Reveal Config Vars, Configure Environment Variables, etc... 

##### Environment variables:

|Variable Name| Description                             | Notes |
|-------------|-----------------------------------------|------ |
|`APP_NAME` | your app name                 | Required|
|`ACCESS_KEY`| your "public" key | Optional, Recommended |
|`SECRET_KEY` | your "private" key | Optional, Recommended |

Setting an access key and secret key will keep unauthorized users from using your app.

#### 7. Once you have set the environment variables restart the application and verify in the logs that it started successfully. It should say SWGOH-Comlink is listening on port xxxx in the log.

_
## START UP HELP BY HOSTING PROVIDER
### Heroku
1. Click the button.
[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://dashboard.heroku.com/new?button-url=https%3A%2F%2Fgithub.com%2Fswgoh-utils%2Fheroku-swgoh-comlink&template=https%3A%2F%2Fgithub.com%2Fswgoh-utils%2Fheroku-swgoh-comlink)

2. Create the application with a unique name and press `Deploy app` button.

3. Once deployed press `Manage App` button under the installation log window.

4. Go to the Settings tab.

5. Press `Reveal Config Vars` button in the Config Vars section and set environment variables.

6. Check to see if the Dyno is running by going to the `Overview Tab` and seeing if it is listed as On under Dyno formation. If it is not, activate it under the `Resources tab` by clicking the slide bar to the right of it.

7. Check logs for any errors by going to `More -> View logs` located in the top right corner of the page.

8. In your Heroku account for this Dyno go to `Deploy`

9. Select `GitHub` as your deployment method and enter your login credentials in `Connect to GIthub`

10. Search for the name of the forked repo and select Connect

11. Any time the version of SWGOH Comlink needs to be updated, go down to the `Manual Deploy` section on the `Deploy`screen, choose the branch and the click `Deploy Branch`

