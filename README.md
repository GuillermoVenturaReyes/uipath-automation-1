# Introductory Email Automation

## Project Description

This program will automate the reptitive process of sending introductory emails to all new batch associates. The automation supports emails with both Zoho and Gmail and can be run either attended, or fully unattended.

## Technolgies Used
* UiPath Studio
* Uipath Orchestrator
* GSuite API
* Windows Credential Manager

## Features
* Interact with Googles interfaces to log in/out of Google accounts, handle two factor authentication and access Gmail using the GSuite API
* Ability to make custom changes to the template message per batch 
* Take in all inputs beforehand in the form of a JSON string to make the process completely unattended. (example below)
```
{
	"BatchName": "TestBatch-65465",
	"Subject": "Welcome to Revature!",
	"EmailTemplateFilePath": "C:\\Users\\<username>\\Documents\\RevatureAutomationFiles\\EmailTemplate.txt",
	"CustomMessage": "",
	"AssociateEmailsFilePath": "C:\\Revature\\201019-UTA0UiPath\\uipath-automation-1\\Data\\Input\\AssociateEmails.xlsx",
	"MailService": "Zoho"
}
```
**BatchName**: *Will be used to create the form for automation-2 and will be used in the intro email*  
**Subject**: *The subject line for the intro email*  
**EmailTemplateFilePath**: *The file path for the email template file to be added to the body of the intro email*  
**CustomMessage (optional)**: *Add a custom message after the email template*  
**AssociateEmailsFilePath**: *The file path to the .xlsx file containing the list of associate emails*  
**MailService**: *The mail service you are sending your introduction emails from. As of now it supports "GSuite" (@gmail.com/@revature.com) and "Zoho" (@revature.net) values*

The file that this JSON string should be stored in is called ```IntroEmailInput``` and the filepath to that txt file should be in a folder called ```RevatureAutomationFiles``` within your Windows machines Document folder. So the full path should look like this: ```/Documents/RevatureAutomationFiles/IntroEmailInput.txt```

If you want the email to use a premade template, you will need to create one as a txt file called ```EmailTemplate.txt```and include it in the RevatureAutomationFiles folder.

## Getting Started
To get this automation running on your machine, you will need to install the Uipath Edge extension as well as setup UiPath Orchestrator or Windows Credential Manager with the following assets
* GoogleCredential
* ZohoCredential
* EmailWorkbookPath
* GSuiteOAuthCredential


###### Email Credentials (Google & Zoho Credential)
* For this step, all you need to do is add the Gmail and Zoho account credentials to Orchestrator as credential Assets or add them to your Windows Credential Manager if you do not want to use Orchestrator.
* For outlook, all that is required is an open Outlook application 
* Due to a recent update to Zoho, credentials must include an application password. Created by going to Zoho, selecting your account. Then selecting the security tab. Select the App Passwords tab, and creating a new app password for your zoho account. This password should be used in place of your actual password to bypass 2FA.

###### Email Workbook Path

* After downloading this automation, Create a xlsx file called 'AssociateEmails.xlsx' and add all the new batch associates email addresses to it under the first column which needs to be named 'Email'.
* The sheet name should just be 'Sheet1' 
* Add 'AssociateEmails.xlsx' to the Input subfolder in the Data folder of the project to configure the workbook path.

###### GsuiteOAuthCredential Setup

* Navigate to Console.Cloud.Google.com
* Click the dropdown box at the top of the webpage marked 'Select a project' and then click the 'Create a new project' button in the top right of the newly opened window.
* Name the project something relevant like UiPath Gsuite, but the name isnt really important.
* Navigate to the APIs & Services Dashboard by clicking on the sidebar option on the left and click the '+ Enable APIs and Services' button at the top of the page. Then search for and enable any APIs you would want your bot to use. In this case, all you will need to enable is the Gmail API.
* Now click on the APIs & Services sidebar button but navigate to the 'Credentials page instead. From here click the '+ Create Credentials' dropdown at the top of the page, select 'OAuth client ID and then click the 'Configure Consent Screen' button.
* Select the 'External' radio button and hit create. Then enter a name to the application being used. You can again just put Uipath Gsuite, then hit save to configure your consent screen. (You may be asked for a contact email too)
* Once again navigate to the APIs & Services Credentials page, click the '+ Create Credentials' dropdown and select 'OAuth client ID.
* Select 'Desktop app' for the application type and give it a name like before and click create.
* Your 'GSuiteOAuthCredentials' will now be displayed on the screen.

###### Uipath extension for Edge

* Make sure you have the UiPath web automation extension enabled on your Microsoft Edge browser. 
* To do this, go to https://docs.uipath.com/studio/v2019-fastTrack/docs/installing-the-edge-extension for a step-by-step guide. (You will need to have studio installed already)
* This will allow the automation to interact with the Edge browser

# First Time Run Notes

###### Consent Screen For Gmail

* The consent screen that was configured in the previous steps will allow you to send emails with Gmail. 
* But the first time you try to do this, you will encounter that consent screen and will need to manually give the bot consent to send emails. 
* You will probably also have to get past the 'This app isn't verified' screen. Just click the Advanced button and then click 'Go to <App name>(unsafe)'. (This is your own application so there is actually no safety concern)
* You wont have to worry about any of this if you are only using Zoho to send the emails.

## Usage

Once You have installed everything, have credentials & workbook path setup and dealt with the consent screen for the first time, you should be able to run the introductory email automation.



