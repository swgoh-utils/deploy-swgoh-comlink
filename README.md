# Deploy SWGOH Comlink to Heroku
This repo is used to create a quick and easy way to deploy and update SWGOH Comlink on Heroku using GitHub.

Visit the main [SWGOH Comlink repo on GitLab](https://gitlab.com/swgoh-tools/swgoh-comlink) to learn more about what SWGOH Comlink is and how to use it.

### Heroku limitations
The free version of Heroku is limited on how much data it can deliver at one time. This means you will have to _request the localization file in zip format_ from the `/localization` endpoint and you must request information from the `/data` endpoint _in segments_, prefereably with `includePveUnits` set to false.

You only get 500 hours for using SWGOH Comlink each month, you must add a credit card to your account to increase it to 900 hours which would allow for it to run 24/7 if needed.

### Comlink limitations
In order to calculate stats for player rosters you must use the roster data with [SWGOH Stats](https://gitlab.com/swgoh-tools/swgoh-stats) which may need to be hosted on a separate Heroku account. You can use the following link to quickly set it up on Heroku: [sw-goh-tools/heroku-swgoh-stats](https://github.com/sw-goh-tools/heroku-swgoh-stats).


## Deploy steps
#### 1. Click the button below.
[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://dashboard.heroku.com/new?button-url=https%3A%2F%2Fgithub.com%2Fsw-goh-tools%2Fheroku-swgoh-comlink&template=https%3A%2F%2Fgithub.com%2Fsw-goh-tools%2Fheroku-swgoh-comlink)

#### 2. Create the application with a unique name and press `Deploy app` button.

#### 3. Once deployed press `Manage App` button under the installation log window.

#### 4. Go to the Settings tab.

#### 5. Press `Reveal Config Vars` button in the Config Vars section and set environment variables.

##### Environment variables:

|Variable Name| Description                             | Notes |
|-------------|-----------------------------------------|------ |
|`APP_NAME` | your app name                 | Required|
|`ACCESS_KEY`| your "public" key | Optional, Recommended |
|`SECRET_KEY` | your "private" key | Optional, Recommended |

Setting an access key and secret key will keep unauthorized users from using your app.

#### 6. Check to see if the Dyno is running by going to the `Overview Tab` and seeing if it is listed as On under Dyno formation. If it is not, activate it under the `Resources tab` by clicking the slide bar to the right of it.

#### 7. Check logs for any errors by going to `More -> View logs` located in the top right corner of the page.


## Updating SWGOH Comlink for new releases
In order to update SWGOH Comlink when a new release comes out you must follow these steps:

#### 1. Create a GitHub account.

#### 2. Fork this repository or copy the files from this repo into a new private repo.
If you Fork this repo it will remain public and others can see the app you have delpoyed it to. It is recommended that you copy these files to a private repo to keep others from using your Dyno hours.

#### 3. In your Heroku account for this Dyno go to `Deploy`

#### 4. Select `GitHub` as your deployment method and enter your login credentials in `Connect to GIthub`

#### 5. Search for the name of the forked repo and select Connect

#### 6. Any time the version of SWGOH Comlink needs to be updated, go down to the `Manual Deploy` section on the `Deploy`screen, choose the branch and the click `Deploy Branch`
