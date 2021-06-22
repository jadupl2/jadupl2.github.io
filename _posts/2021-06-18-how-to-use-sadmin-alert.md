---
title:          How-to use SADMIN alerting system
desc:           Using SADMIN alerting system
version:        2.2
summary: |         
    Page under construction, should be completed soon, come back later.
    {: .text-justify}
updated:        2021-06-18
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

### Requirements:

- If you want to use "Slack" as your alerting method, you need a [Slack workspace](https://slack.com/signin#/signin)
  - If you don't have one, you should read our [How-to create a Slack workspace]({% post_url 2021-06-16-sadm-create-slack-workspace %}) page and create one.
  - You will also need at least one channel and one Slack App. in order to receive alert on your channel.
  - If you don't, have a look at the page [How-to create Slack channel and App.]({% post_url 2021-06-17-sadm-create-slack-channel-and-slack-app %}).
- If you want to use the SMS method for alerting, see [How-to setup SMS notification](/how-to/how-to-sms) page before.
- If you want to use email alerting system, make sure you have valid email(s) address in the [SADMIN configuration file]({% post_url 2021-04-26-sadmin-cfg %}#sadm_mail_addr) .
- You'll need your favorite editor, to modify some configuration files and to create a test script.

{: .text-justify}
 

[Back to the top](#top_of_page)



<a id="seealso"></a>
## SEE ALSO

| Link to ...| Description |  
| :--- | :--- |  
| [sview]({% post_url 2021-05-18-sadm-sysmon-tui %})                   |  Command line summary of alerts and failed scripts of all your servers.  
| [sadm_daily_report]({% post_url 2021-04-01-sadm-daily-report %})                  | Produce and email monitoring daily reports
| [sadmin.cfg]({% post_url 2021-04-26-sadmin-cfg %})                                | SADMIN main configuration file   
| [sadm_sysmon.pl]({% post_url 2021-06-10-sadm-sysmon %})                           | Client system monitor   
| [sadm_fetch_client.sh]({% post_url 2021-03-16-sadm-fetch-client %})               | rsync all .rch/.log/.rpt from actives clients to the SADMIN server  
| [SysMon configuration file]({% post_url 2021-06-11-sadm-sysmon-config %})         | Client System Monitor configuration file     
| [smon]({% post_url 2021-06-15-sadm-sysmon-cli %})|   Allow you run SysMon and see the report file |   
| [How-to create a Slack workspace]({% post_url 2021-06-16-sadm-create-slack-workspace %}) | Create a Slack Workspace |    
| [How-to create Slack channel and App.]({% post_url 2021-06-17-sadm-create-slack-channel-and-slack-app %}) | Configure Slack Channel |   
| [How-to use SADMIN alerting system]({% post_url 2021-06-18-how-to-use-sadmin-alert %}) | Understanding SADMIN alerting system |  

