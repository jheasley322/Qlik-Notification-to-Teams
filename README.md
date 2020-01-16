# Qlik-Notification-to-Teams
 basic qlik app script for getting a list of failed tasks to a channel in ms teams


This app performs a very helpful function of notifying you when there are failures based on 
a task running an app and reading the current task status list.  it only takes a couple of
minutes to execute, so it can run as often as youd like.  i have found that every 20 mintes 
is a really productive cadence.

this can be used AS-IS with very few changes if you are not comforatble with scripting. you
will have to set the following variables specific to your environment:

variables related to when the app should run:
    iDayStart = set to 1 hour before you want notifications to start
    iDayEnd = set to 1 hour after you want notifications to stop
    iWeekday = leave this alone if you want it to run M-F, if you want 
        it to run EVERYDAY, just change the whole thing to "Let iWeekday = 1"
    iRuntime = leave this alone if you want the app to only notify 
        using the above parameters, to make it ALWAYS run, change 
        it to Let iRuntime = 'yes'

Environment Based Variables
    pLib = the name of the data connection you created
    WebHookAddress = the complete wqebhook address given 
        to you by teams during setup
    iEnvironment = set up your own logic to determine which environment
        the app is running in. if all of your nodes are named using a
        consistent naming convention, this is easier
    iColor = hex color values for the different outputs of iEnvironment

The app only reviews failures on the cluster in which it runs. if
you have multiple clusters, the app needs to be loaded on each one
and scheduled to run. you can run the exact same app on all clusters.

Instructions for setup:
1. Generic REST Connector - set up a generic REST connection specific to 
    posting out json through a webhook. i used:
        "https://jsonplaceholder.typicode.com/posts"
        method: post
        authentication: anonymous
        allow response headers: yes
   the name of this connection will be used in a variable

2. Teams Webhhook - follow the prompts in teams to set up a new webhook.
    Make sure you know WHERE you want the notifications to go before you 
    start, as this is one of the questions that will be asked. copy the
    address given at the end of the process, will be used in a variable

3. Script - update all required variables in the app script

4. App(s) - create an app in each environment that uses the completed 
    script.  schedule the app to run at whatever cadence works for you.