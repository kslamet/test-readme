# Segment Setup for StrangePalooza Project

## What is it

This writeup describes how to setup your Segment account so that you are able to use the necessary features required for the StrangePalooza project.
This is in no way a best practice for setting up a Segment Workspace and project.
For Segment documentation, please refer to https://segment.com/docs/ 

A few configurations to expect in this setup:

- Javascript Website Source setup
- Salesforce destination setup
- Custom Function: Send WhatsApp Message using Twilio

## Prerequisites

You need to request for the following from #provisioning slack thread:

- Upgrade to business / employee account
- Enable personas, journeys
- Enable custom functions
- Recommended: increase account MTU to 10000
- Provide slug. You can find this general settings tab in https://app.segment.com/your-workspace-name/settings/basic

![slug](https://emerald-stingray-3654.twil.io/assets/Slug.png)

Other things you need:
A developer version of Salesforce.com. To sign up for one, go to https://developer.salesforce.com/signup

## Create Javascript Source

Steps:
- Go to Connections -> Sources -> Add Source
- Select Javascript -> Add Source
- Give it a name, and hit Add Source

![js_source](https://emerald-stingray-3654.twil.io/assets/Javascript%20Source.png)

## Update Analytics.js write code and Flex Webchat IDs in index.html

Steps:
- Open index.html on a code editor
- Copy the write code from your Javascript Source
- Replace the existing write code in index.html
- Update the Account Sid and Flex Flow Sid for the Flex Webhat widget
- Save the index.html page
- Open the index.html page and test out the button a few times

![writecode](https://emerald-stingray-3654.twil.io/assets/Write%20Code.png)

## Create Salesforce Destination

Steps:
- From Javascript source, hit Add Destination and search for Salesforce CRM
- Hit Configure Salesforce
- Provide a destination name e.g. Demo and hit save
- Provide your username, password and security token
- Under other settings, ensure Always Enabled is On
- Click on Actions, and fill out the sections as shown below
- Hit save and activate the integration

![SalesforceSettings](https://emerald-stingray-3654.twil.io/assets/Salesforce%20Settings.png)

## Create Custom Destination Function
- Go to Connections -> Destinations, go to Functions tab and hit New Function
- On the right panel, choose Templates and select Twilio
- Update the javascript code on the left as you like
- On the right panel, under settings, input Twilio Account Sid, Access Token and either twilioFrom in +xxxx format or twilioWhatsAppFrom in whatsapp:+xxxx format
- Optional: hit the Settings tab and add the WhatsApp logo
- Hit save and deploy

![WhatsappCustomFunction](https://emerald-stingray-3654.twil.io/assets/Whatsapp%20Custom%20Destination.png)

![WhatsappCodeSample](https://emerald-stingray-3654.twil.io/assets/Whatsapp%20Code%20Sample.png)

## Setup Persona and Journeys
- Select default identifier and use email
- Add Javascript Source above as your source
- Create new audience, with criteria All Users who performed join_livestream at least 1 time
- Select your whatsApp destination, and hit review and create
- Set your audience name, and hit Create Audience
- On the Journeys tab, hit New Journey
- Set entry condition to import audience from the one you just created, and make sure Use Historical Data for Entry Step is checked
- Add a new step -> Send to Destinations
- Populate the Step name
- Hit Connect destination -> Select WhatsApp -> ensure Send Track is activated and add 1 destination
- Hit Save, then hit Publish

![journey](https://emerald-stingray-3654.twil.io/assets/Journey.png)

That's it! Go make changes and have fun!
