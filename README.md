 [![Linux](https://img.shields.io/badge/platform-linux--64-brightgreen)](https://ubuntu.com/download/desktop)  [![Live Dashboard](https://img.shields.io/badge/Live%20-Dashboard-green)](https://cognitive-social-crm-persistent-quokka-ch.eu-gb.mybluemix.net/) [![Twitter Bot](https://img.shields.io/twitter/follow/HealthMessiah?style=social)](https://twitter.com/HealthMessiah)
# <img src="doc/source/images/logo (1).png"  alt="Covid MentAid logo">

Covid MentAid uses various IBM Technologies to analyze sentiment of the tweets of the public from all over the world during the covid19 Pandemic. The resulting analysis is presented in a Live web-framework (dashboard) as a series of graphs and charts and a Twitter bot which replies to people’s tweet which indicates fear, sadness, scared with funny memes/gifs/motivating pics from Reddit.

## Team Name: - X Æ A-4

## Get Started

1. [Short description](#short-description)
1. [Youtube video](#youtube)
1. [PPT](#power-point-presentation)
1. [Live App Link](#live-app-link)
1. [Flow of the Project](#flow)
1. [Included components](#included-components)
1. [Featured technologies](#featured-technologies)
1. [Steps to run the Dashboard (UBUNTU-Angular)](#steps-for-dashboard)
1. [Steps to run the Twitter Reddit Bot (Python)](#Steps-to-run-the-twitter-bot)
1. [Results](#results)
1. [Contributors](#contributors)

## Short description

### What's the problem?

COVID-19 outbreak was first reported in Wuhan, China, and has spread to more than 50 countries. WHO declared COVID-19 as a Public Health Emergency of International Concern (PHEIC) on 30 January 2020. Currently, people are staying inside their homes for 4 months for self-quarantine purposes. This has led to a sharp increase in mental health problems and suicide rates all across the globe.

[![Blog](doc/source/images/BigB.png)](https://www.thehindu.com/sci-tech/health/coronavirus-amitabh-bachchan-on-how-covid-19-takes-toll-on-patients-mental-health/article32196416.ece)

### The idea

In this project, our server application subscribes to a **LIVE** Twitter feed with hashtags of "Covid19". Each tweet received will be analyzed for emotional tone and sentiment, and the intent of the tweet will be determined by the Watson Assistant service. All data is stored in a Cloudant database. The resulting analysis is presented in a web-framework (dashboard) as a series of graphs and charts.

In addition to this, we have a **Twitter Bot** which replies to people’s tweets which indicates fear, sadness, scared with funny memes/gifs/motivating lines and a hotline for suicide help based on their geo-location supplied by twitter API. 

## Youtube
[![Watch the video](doc/source/images/youtube.jpeg)](https://www.youtube.com/watch?v=c_A3PlL_CD4 )

## Power Point Presentation
[PPT](https://docs.google.com/presentation/d/1jmZPiED1og-pp8xrOop7LF5duuyV_En8pUSGLsnfLi4/edit?usp=sharing)

## Live app link
> Note: - The link may or may not be active. We are using the free plan of IBM cloud service and as this project takes LIVE tweets this requires us to change the api credentials after certain period of time based on the number of tweets stored in the cloudant. 

> If you want to see the live demo, refer the youtube link given above or contact us to on the website at `2018.abhay.gupta@ves.ac.in`

[Dashboard Link](https://cognitive-social-crm-persistent-quokka-ch.eu-gb.mybluemix.net)


## Flow

![](doc/source/images/architecture.png)

1. Tweets are pushed out by Twitter.
2. The Sentiment Analysis of COVID-19 Tweets app processes the tweet.
3. The Watson Tone Analyzer Service performs analysis of sentiment and emotional tone.
4. The Watson Natural Language Understanding Service pulls out keywords and entities.
5. The Watson Assistant Service extracts the intents (verbs) from the tweets.
6. Tweets and metadata are stored in Cloudant
7. The dashboard displays charts and graphs as well as the tweets.

## Included components

- [Watson Assistant](https://www.ibm.com/cloud/watson-assistant/): Watson Assistant is a robust platform that allows developers and non-technical users to collaborate on building conversational AI solution.
- [Watson Tone Analyzer](https://www.ibm.com/watson/services/tone-analyzer): Uses linguistic analysis to detect communication tones in written text.
- [Watson Natural Language Understanding](https://www.ibm.com/watson/services/natural-language-understanding): Natural language processing for advanced text analysis.
- [IBM Cloudant](https://www.ibm.com/cloud/cloudant): A managed NoSQL database service that moves application data closer to all the places it needs to be — for uninterrupted data access, offline or on.
- [Cloud Foundry](https://www.cloudfoundry.org/): Build, deploy, and run applications on an open source cloud platform.

## Featured technologies

- [Artificial Intelligence](https://medium.com/ibm-data-science-experience): Artificial intelligence can be applied to disparate solution spaces to deliver disruptive technologies.
- [Databases](https://en.wikipedia.org/wiki/IBM_Information_Management_System#.22Full_Function.22_databases): Repository for storing and managing collections of data.
- [Angular](https://angular.io/): A framework to build UI for mobile and desktop application.
- [Node.js](https://nodejs.org/): An open-source JavaScript run-time environment for executing server-side JavaScript code.
- [Express](https://expressjs.com/): Fast, unopinionated, minimalist web framework for Node.js

# Steps for dashboard

We can deploy the code to IBM Cloud (or run the code locally, there will be one more step to configure the credentials locally.)

1. [Install Dependencies](#1-install-dependencies)
2. [Twitter Requirements](#2-twitter-requirements)
3. [Create Watson services with IBM Cloud](#3-create-watson-services-with-ibm-cloud)
4. [Import the Assistant workspace](#4-import-the-assistant-workspace)
5. [Configure credentials](#5-configure-credentials)
6. [Run the application](#6-run-the-application)

### 1. Install dependencies

The application requires the following software to be installed locally.

1. [Node (6.9+)](https://nodejs.org): Application runtime environment, download and install the package.
2. [Angular CLI (6.1.1)](https://www.npmjs.com/package/@angular/cli): A CLI for Angular applications, installed with: `npm install -g @angular/cli`.
3. [Angular (6.1.0)](https://angular.io): Angular will be added as a dependency of client in `package.json` when setting up client using `Angular cli`.
4. [Express (4.16.3)](https://expressjs.com): Express will be added as a dependency in `package.json` for server.

> If you have Angular CLI already installed. Please read the upgrade instructions for Angular CLI when you upgrade the software.

Run the following command, from the application folder, to install both the client and server dependencies.

```
$ npm run app-install
```


### 2. Twitter requirements

To subscribe to Tweets from a specific handle or hashtag in this application, it is required to create a Twitter account and a Twitter application.
The Twitter account will be used as the account that receives the messages from other Twitter users as well as the owner of the application, required by Twitter, to receive Tweets.

- You can create a normal Twitter account on [Twitter](https://twitter.com/signup) or use an existing account. It is required to provide a unique email id that isn't already associated with an existing Twitter account as well as a phone number to verify the account.
- Once you have the Twitter account created and verified, log in to [Twitter Dev](https://developer.twitter.com/apps) and create an application.
- Select the Keys and Access Tokens tab and generate a Consumer Key and Secret.
  Keep this page open as you will need to use these tokens into setup procedure in the application later on.

### 3. Create Watson services with IBM Cloud

Either Setup the IBM Cloud Deployment or Setup Local Deployment.

#### Setup local Deployment

> Create the IBM Cloud services and configure them to use on a locally running server app.

If you do not already have a IBM Cloud account, [signup for IBM Cloud](https://cloud.ibm.com/registration).
Create the following services:

- [**Watson Assistant**](https://cloud.ibm.com/catalog/services/watson-assistant-formerly-conversation)
- [**Watson Tone Analyzer**](https://cloud.ibm.com/catalog/services/tone-analyzer)
- [**Watson Natural Language Understanding**](https://cloud.ibm.com/catalog/services/natural-language-understanding)
- [**IBM Cloudant DB**](https://cloud.ibm.com/catalog/services/cloudant)

>NOTE: When provisioning Cloudant, for `Available authentication methods` choose `Use both legacy credentials and IAM`


### 4. Import the Watson Assistant skill

- Find the Assistant service in your IBM Cloud Dashboard.
- Click on the service and then click on `Launch tool`.
- Go to the `Skills` tab.
- Click `Create new`
- Click the `Import skill` tab.
- Click `Choose JSON file`, and upload [this](data/assistant/workspace-social-crm-airline-classification.json). the workspace.json file in 
- Select `Everything` and click `Import`.

To find the `WORKSPACE_ID` for Watson Assistant:

- Go back to the `Skills` tab.
- Click on the three dots in the upper right-hand corner of the app and select `View API Details`.
- Copy the `Workspace ID` GUID.

### 5. Configure credentials
Fill in the requried details needed in the server/env.sample

Change it's name to ".env"

This is to be done before executing on the IBM server.

> The `.env` file is where all the parameters like credentials, log settings and other constants required by this application is kept.

#### Configure service credentials

The credentials for IBM Cloud services (Tone Analyzer, Natural Language Understanding, and Cloudant), can be found in the `Services` menu in IBM Cloud, by selecting the `Service Credentials` option for each service.

> NOTE: When provisioning Cloudant, for `Available authentication methods` choose `Use both legacy credentials and IAM`

From the root of the project, go to `server` folder (`cd server`) and

Add all the credentials that you have saved from creating the services, as explained earlier, in the `.env` file.

### 6. Run the application

Either `Run the app on IBM Cloud` or `Run the app locally`.

#### Running the app on IBM Cloud

1. Compile the Angular client code and Express server code using the following command. This creates a `dist` folder in your project root directory and copies the compile code and necessary files to be deployed to IBM cloud.

```
$ npm run build
```

2. Connect to IBM Cloud in the command line tool and follow the prompts to log in

```
$ ibmcloud cf login -a https://api.ng.bluemix.net
```

> Make sure you set the `target` and `space` correctly using `ibmcloud target -o <target> -s <space>`

3. Push the app to IBM Cloud.

```
$ ibmcloud app push
```

4. The application should now be running on IBM Cloud and listening to Tweets. You can get the application URL by going to `Cloud Foundry Applications` section of IBM cloud dashboard. Click the name of the application you just pushed and clikc `Visit App URL` to access the application.

#### Running the app locally

Once all the credentials are in place, the application can be started with:

```
$ npm run start
```

The server runs on port `3000` and the `client` runs on port `4200`. You can access the UI by accessing the following URL in the browser:

`http://localhost:4200`

# Steps to run the twitter Bot
## What our bot actually does?
- Our bot replies to original tweets of user using a particular hashtag(eg: #Covid19) which it detects sad using the IBM watson tone analyzer with a motivation pic using the reddit api from the subreddit MotivationalPics.
- Twitter Handle of the bot: - [profile](https://twitter.com/HealthMessiah)

## Note: - Navigate to the TwitterBot-final folder.
## Note: - Python 3 is used here.

### 1. Adding the required Keys to keys.py file
- Twitter Keys: Use the previously created twitter dev acc's keys or [make new one](https://apps.twitter.com/) and use them to fill the consumer_ket, consumer_secret, access_token, access_token_secret fields.
- Ibm Keys: Create a new tone analyzer service using a new [IBM cloud account](https://www.ibm.com/watson/services/tone-analyzer/) and use these to fill ibm_key, ibm_url fields.
- Reddit Keys: Create a [reddit api](https://www.reddit.com/prefs/apps/) and use the given keys to fill the C_id, C_secret, User_agent, Uname, Password. Note: User_agent: can be any string, it's a description of ur app,, Uname: username use to login on reddit,, Password: main password of your reddit account, C_id is the first yellow box and C_secret is the second yellow box as shown: -
![](doc/source/images/redditKeys.png)

### 2. Running the py files: -
- Use `pip install -r requirements.txt` to install all the dependecies.
- run the tempBot.py program to start the bot.

## Note: - To change the hashtag it follows, change the hashtag on line number 46 in tempBot.py
## Note: - To change subreddit from which the reddit bot gives posts, change the name on line number 20 in reddit_twitter_bot.py
## Note: - To host the bot to run 24/7 we reccomend [python anywhere](https://www.pythonanywhere.com/) (use `pip3` to install and `python3` on it's console to run the files.
# Results

You will see informations about Tweets:

![](doc/source/images/homePage.jpeg)

as well as Classification of live tweets, Sentiment over time, Emotional Tone over time, and Keywords mentioned:

![](doc/source/images/tweetPage.jpeg)

Twitter bot replying to sad/depressed tweets with motivational pics/quotes:

![](doc/source/images/tweets.jpeg)



## Contributors
Jay Jhaveri: https://github.com/JayJhaveri1906

Prem Chhabria: https://github.com/premchhabria

Abhay Gupta: https://github.com/abhay8463

Neeraj Ochani: https://github.com/neeraj0008

Prasad Govekar: https://github.com/govekarmohit





