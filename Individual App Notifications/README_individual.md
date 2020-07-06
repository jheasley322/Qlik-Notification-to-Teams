# Qlik-Notification-to-Teams
 basic qlik app script for getting a list of failed tasks to a channel in ms teams


This app performs a simple Teams Channel notification whan an app has reloaded.  This
notification is part of the app execution and NOT tied to the task. This can be particularly
helpful when developing scrips that are reloaded from the QMC and take a long time.

This can be used as a copy/paste into any app script as the last portion of the script. A more
efficient way of utilising this is with the Include or Must_Include function in your app; allowing
a single line of text to be added to any app to initiate the notification.

this can be used AS-IS with very few changes if you are not comforatble with scripting. you
will have to set the following variables specific to your environment:


Environment Based Variables
    pLib = the name of the data connection you created

    WebHookAddress = the complete wqebhook address given 
        to you by teams during setup

    iEnvironment = set up your own logic to determine which environment
        the app is running in. if all of your nodes are named using a
        consistent naming convention, this is easier

    iColor = hex color value for the notification
    
    qmc = this is a variable that will pass a link to the QMC tasks page into your notification.
        update the variable text to include your domain in order to pass a functioning link.

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

4. App - 
    option 1: copy and paste this script into the end of the application load script
    option 2:
        a. store the script into a text file that is accessible to your Qlik Server
        b. use the include/must_include function to access the script:
            example: $(Must_Include='lib://your_library_name/your_library_path/app_notification_script.txt');



Happy Notifying!!!
-joe easley-