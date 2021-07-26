---
title:          How-to create a Slack workspace
desc:           Create a Slack Workspace
version:        1.2
summary: |         
    In this guide, we will show you how to [create your own Slack workspace](https://slack.com/get-started#/createnew) (It's free).
    {: .text-justify}
updated:        2021-06-16
os:             Linux
type:           D  # [D]oc [S]=Server only [C]=Client [B]oth
categories:     [ system_monitor ] 
tags:           [ system_monitor ] 
#
layout:         single
search:         true
author_profile: false
toc:            false
classes:        wide
sidebar:
  title:        "Documentation"
  nav:          sidebar-manpage
---
<a id="top_of_page"></a>
{{ page.summary }} 
- The next step after creating your Slack workspace, is to create some channel(s).
- They will be use to receive alert issued by your scripts and by the SADMIN Monitoring System.
- Once your workspace is created, please see our [How-to create and use Slack channel page]({% post_url 2021-06-17-sadm-create-slack-channel-and-slack-app %}).
- But first, let's create our Slack workspace.
- Visit this [page](https://slack.com/get-started#/create) to initiate the creation of your workspace.


First you need to enter your email address. 

![Create Slack Workspace](/assets/img/sadm_slack/slack_enter_email.png){: .align-center} 


Shortly after that, the screen below will appear.
You should have received an email from Slack with a confirmation code, that you need to enter here.
This will confirm that the email you've given is yours. 

![Enter email for Slack](/assets/img/sadm_slack/slack_confirm_email.png){: .align-center} 


Enter your name, so that people in your workspace can identify you.
Uncheck the check box below your name if you don't want to receive email about Slack service. 

![Enter your name for Slack](/assets/img/sadm_slack/slack_enter_name.png){: .align-center} 


Set your password for Slack.

![Enter password for Slack](/assets/img/sadm_slack/slack_enter_password.png){: .align-center} 


Enter your Company name or a Group name of your choice. 

![Enter Group Name for Slack](/assets/img/sadm_slack/slack_cie_name.png){: .align-center} 



Enter the URL name you want to use to access your workspace.
This is will constitute the URL you'll use to access your workspace.
For example, if you enter 'sadm_alert' as your URL name, you would access your workspace 
by entering this URL "https://sadm_alert.slack.com".

![Enter Slack URL](/assets/img/sadm_slack/slack_workspace.png){: .align-center} 


Finally, you can invite some friends or coworkers to join and use your workspace.
The people you invite, will be able to see, add and comment on the messages in your workspace.
You can skip the invitation screen (you can do it later), by pressing the "Skip for now" button. 

![Slack Invitation](/assets/img/sadm_slack/slack_send_invitations.png){: .align-center} 


This is it, you now have your own Slack workspace.

You can use [Slack via the Web](https://slack.com/intl/en-ca/) or by using their application that run on the platform of your choice;
- [MacOS](https://slack.com/intl/en-ca/downloads/mac)
- [Windows](https://slack.com/intl/en-ca/downloads/windows)
- [Linux](https://slack.com/intl/en-ca/downloads/linux)
- [iOS](https://slack.com/intl/en-ca/downloads/ios)
- [Android](https://slack.com/intl/en-ca/downloads/android)

Please see our [How-to create and use Slack channel page]({% post_url 2021-06-17-sadm-create-slack-channel-and-slack-app %}).

[Back to the top](#top_of_page)



<a id="seealso"></a>
## SEE ALSO

| Link to ...| Description |  
| :--- | :--- |  
| [sview]({% post_url 2021-05-18-sadm-sysmon-tui %})                   |  Command line summary of alerts and failed scripts of all your servers.  
| [sadm_daily_report]({% post_url 2021-04-01-sadm-daily-report %})                  | Produce and email monitoring daily reports
| [sadmin.cfg]({% post_url 2021-04-26-sadmin-cfg %})                                | SADMIN main configuration file   
| [sadm_sysmon.pl]({% post_url 2021-06-10-sadm-sysmon %})                           | Client system monitor   
| [sadm_fetch_clients.sh]({% post_url 2021-03-16-sadm-fetch-clients %})               | rsync all .rch/.log/.rpt from actives clients to the SADMIN server  
| [SysMon configuration file]({% post_url 2021-06-11-sadm-sysmon-config %})         | Client System Monitor configuration file     
| [smon]({% post_url 2021-06-15-sadm-sysmon-cli %})|   Allow you run SysMon and see the report file |   
| [How-to create a Slack workspace]({% post_url 2021-06-16-sadm-create-slack-workspace %}) | Create a Slack Workspace
| [How-to create Slack channel and Slack App.]({% post_url 2021-06-17-sadm-create-slack-channel-and-slack-app %}) | Configure SADMIN to use Slack|)
| [How-to use SADMIN alerting system]({% post_url 2021-06-18-how-to-use-sadmin-alert %}) | Understanding SADMIN alerting system |  
