# google-fitbit-autosave

I fell in love with my Fitbit again after I started collecting granular intraday heartrate data. Now I not only enjoy the device and standard data visualizations from fitbit.com and the fitbit app, but also I get to play around with some pretty detailed data!

The path to full functionality here was a hybrid of (1) Simon Bromberg's code, (2) Jozef Jarosciak guide (helps avoid an important pitfall in Bromberg's ReadMe file), and (3) a bit of code I wrote myself (autosave functionality).

In large part, the following guide is an adaptation of Jozef Jorosciak's excellent tutorial here: https://www.joe0.com/2017/03/18/how-to-sync-fitbit-data-to-google-spreadsheet, although I've found that heartrate.gs works better than intraday.gs.

The following article is a step by step guide on how to sync Fitbit intraday heartrate data into a Google spreadsheet. This heartrate data should be granular to around every 6-10 seconds.

This method of synchronizing Google Spreadsheet with Fitbit data is based on the work of Simon Bromberg. It uses a new Fitbit OAuth2 and Google’s OAuth2 authentication method (tested as of 18.March.2017). You can find more about the sync scripts here: https://github.com/simonbromberg/googlefitbit

Copy Heartrate.gs script
Visit following URL and put the content of the heartrate.gs script into your clipboard (CTRL: https://github.com/simonbromberg/googlefitbit/blob/master/heartrate.gs (or if you want autosave functionality, instead, copy the heartrate.gs script in this repository: https://github.com/JoelDoerfel/google-fitbit-autosave/blob/mastery/heartrate.gs)

Create a new Google Spreadsheet
As a first step, create a new Google spreadsheet, name it whatever you want and save it.

Add heartrate.gs script to Google Spreadsheet
Then go to ‘Tools’, select ‘Script Editor’ option.

Paste the contents of the heartrate.gs file into the script editor, overwriting whatever default function definition is already in there. Then name it and save the document.

Now, return to your blank spreadsheet (you can close the script window) and press F5 to refresh the page. It’ll take about 5 seconds after the refresh for the ‘Fitbit’ menu to show up at the top of the Google spreadsheet menu. 

Install OAuth2 library for Google Apps Script
Now go to ‘Tools,’ select ‘Script Editor’ again. We’ll need to add the Oauth2 Google Script library to our spreadsheet. To do so, click Resources in the top menu, then select Libraries:

Then add the OAuth2.0 library by typing in the project key “MswhXl8fVhTFUH_Q3UOJbXvxhMjh3Sh48” and hitting the Add button:

Once done, select the newest version and development mode and press save. 

Get the ‘Script ID’
The past procedures required a to get a project’s key by clicking on the ‘Fitbit’ menu inside the spreadsheet and clicking ‘Setup.’

However, the new process no longer uses the Project Key, which is deprecated now.

Instead, we’ll need to get a ‘Script ID’. To find it, go to ‘Tools/Script Editor’ again and then select ‘File/Project Properties’:

Copy the text adjacent to ‘Script ID’ in the popup. We will need that in subsequent steps.

Authorize Fitbit Sync
Close the Script Editor and go back to your blank Google spreadsheet and select the FitBit menu and click on ‘Setup’:

A popup window will ask for Authorization:

Click on ‘Continue’ button and follow Google singing process under which you want to authorize the Fitbit syncing application on.

Then it will show you the permissions the application is requesting, click ‘Allow’.

Then the ‘Setup Fitbit Download’ panel should appear. Just close it for now.

Setup a new Fitbit app at Dev.Fitbit.com
Now, go to https://dev.fitbit.com/ and either register a new account or login to your existing account.

Click on ‘Manage My Apps’ in the top menu and click on the ‘Register a New App’ option:

The next step is to fill up the application. You can use whatever data you wish.

These are the important parts:

For the OAuth 2.0 application type option, select: ‘Personal’ option.
Default access type should be set to: ‘Read-Only’.
The other important piece of data on the form is the Callback URL. Type in the following url: https://script.google.com/macros/d/YOUR_SCRIPT_ID/usercallback. Then replace YOUR_SCRIPT_ID in the URL with the Script ID we have gathered in the previous step.
Once done, just press the ‘Save’ button.

On the next page, Fitbit will ask you to Agree to the terms, and Register.

Do so, and you will be redirected to a page that contains your credentials.

Make a note of your ‘OAuth 2.0 Client ID’ and your ‘Client Secret’ keys. 

Setup a Fitbit sync
Go back to your blank Google Spreadsheet and select ‘Setup’ from the ‘Fitbit’ menu.

Copy in the ‘OAuth 2.0 Client ID’ and the ‘Client Secret’ from the previous step. and your project key from step 3.

Select all the activities that you’d like to sync to your spreadsheet. You can select all of them or individual ones.

Then select the range for which to download the data. Just note, that you shouldn’t try to download more than a couple months worth of data, Fitbit’s API will not like you.

Click ‘Save Setup’ and the panel will disappear.

Authorize Fitbit
In your spreadsheet, click ‘Authorize’ from the Fitbit menu and a sidebar will show up on the right.

Click the word ‘Authorize’ in the sidebar.

A page will open up with the Fitbit login page. Log in to the Fitbit account you would like to download data from in the new window, authorize the application by clicking ‘Allow’, and then close the tab when it says “Success you can close this tab”

First Sync
Inside the Google Spreadsheet, click on the Fitbit menu and select the ‘Sync’ option.

The process of synchronization will start.

"Sync & Save" option:

Find a folder in which you'd like to save your daily Fitbit data. 

Go to the Google Script Editor toward the very end of the code (in mine, it's line 379) and update the variable "destFolder":

  var destFolder = DriveApp.getFolderById("{YOUR_DESTINATION_FOLDER}"); 
  
Hit save. Go back to Google Sheets and hit refresh. 

Inside the Google Spreadsheet, once it reloads,  click on the Fitbit menu and select the ‘Sync & Save’ option.

Voila! You're done.

* Philosophical disclaimer: every piece of working code or software, and every app exists to provide humans a functionality that would not exist in that precise form without it. Code creates functions that extend human agency.
