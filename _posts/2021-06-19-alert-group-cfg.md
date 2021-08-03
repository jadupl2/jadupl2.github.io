---
title:          alert_group.cfg
permalink:      /alert-group-cfg/
desc:           SADMIN alert group definition file
version:        2.2
summary: |         
    This is the default alert group definition file.
    {: .text-justify}
updated:        2021-04-22
os:             Linux
type:           D  # [D]oc [S]=Server only [C]=Client [B]oth
categories:     [ configuration-files ] 
tags:           [ configuration-files ] 
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
 
```bash
#========================================================================================
# SADMIN Alert Group file definition  v 2.3
#========================================================================================
# This file is use when an Error or a Warning is detected by SADM System Monitor or 
# when a script need to send an Alert. The scripts (Shell and Python) and SADMIN 
# System Monitor sent alert to an alert group defined in this file.
#
# - If the Alert Group file ($SADMIN/cfg/alert_group.cfg) file doesn't exist then it's 
#   created from the default Alert Group file ($SADMIN/cfg/.alert_group.cfg).
# - Blank line or line beginning with a pound sign (#) are ignored.
# - Field delimiter is a space.
# - Each Alert Group Name MUST be unique and cannot contain spaces.
#
# FIRST COLUMN - GROUP NAME***
# - Alert Group name is use in the SysMon (hostname.smon) config file to designated 
#   who to alert.
# - Alert Group name MUST be unique within this file and can used up to 15 
#   characters (No Space).
#
# - USING ALERT GROUP IN SCRIPT (Shell/Python)
#   - You specify the Alert Group by changing the line(s) below in the SADMIN
#     section at the beginning of your script.
#     Shell Script :
#         export SADM_ALERT_TYPE=3        # 0=NoAlert 1=OnlyOnError 2=OnlyOnSucces 3=Always
#         export SADM_ALERT_GROUP="default" # AlertGroup name for Alert (alert_group.cfg)
#     Python Script :
#       st.cfg_alert_type   = 1         # 0=NoAlert 1=OnlyOnError 2=OnlyOnSucces 3=Always
#       st.cfg_alert_group  = "default" # AlertGroup name for Alert (alert_group.cfg)
#
# - USING ALERT GROUP IN SADMIN SYSTEM MONITOR
#    - You specify the Alert Group you want to use for System Monitor Warning in 
#      column J and for Error in column K. In the example below, we use alerting 
#      group 'sdevops' for Warning and 'sprod' for Error.
#    - Example of a ping test in line a hostname.smon of a client.
# Column 1            2 3  4  5  6    7   8   9 A B C D E F G    H       I     J     K    L
# ping_www.google.com 0 = 01 00 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 sdevops sprod -
#    - If Alert group used in SysMon configuration don't exist in this file, the default 
#       group ('default') is use.
#
# SECOND COLUMN
#   - This column can have the values a 'm', 't' and a 's' (Lowercase/Uppercase allowed)
#   - If it contain other value then 'm' is assumed.
#   - This column specify the alert group type :
#       - 'm' Specify a Mail Group.
#       - 's' Specify a Slack Group .
#             For now only one slack channel can be use per group (change will come)
#       - 't' Specify a SMS (Texto) Group.
#
# THIRD COLUMN
#   - For Alert of type 'm' (Email) :
#       - Email address(es) corresponding to the mail group in column one.
#       - If you specify more than one email address, they must be separated by a comma.
#   - For Alert of type 's' (Slack) :
#       - Slack Channel defined in SADMIN Slack Channel File.
#       - Channel name used MUST be define in the Slack Channel file (alert_slack.cfg).
#       - For now only one slack channel can be use per group (change will come)
#   - For Alert of type 't' (Texto, SMS) :
#       - Third column is use to group cellular number together to form an alert Group.
#         If more than one is specified, they must be separated by a comma.
#
#========================================================================================
# The 'default' Alert Group MUST always exist and MUST refer to Email, Slack, Texto group
#default             t   sms_network
default             m  e_sysadmin
#default             s    sprod

# Email Alert Group
e_sysadmin          m   jacques.duplessis@videotron.ca
e_webteam           m   jacques.duplessis@videotron.ca,support@sadmin.ca

# SMS (Texto) Alert Group, members are Cellular name
sms_sysadmin        t   cell_support
sms_network         t   cell_support,cell_telecom
sms_emergency       t   cell_support,cell_telecom,cell_custsup

# Cellular number of individual (Use only in SMS alert group)
cell_support        c   5147577206
cell_telecom        c   5147560069
cell_custsup        c   4507570068
cell_support_1      c   4187779302
cell_support_2      c   5147779303

# Slack Alert Group
# 3th column is the channel name defined in Slack Alert file (alert_slack.cfg).
sdev                s   sadm_dev
sprod               s   sadm_prod
sinfo               s   sadm_info
sdevops             s   sadm_devops
```

[Back to the top](#top_of_page)

<a id="seealso"></a>
## SEE ALSO

| Link to ...| Description |  
| :--- | :--- |  
| [SADMIN installation](/_pages/install)  | SADMIN installation page |   
| [How-to update SADMIN]({% post_url 2021-03-14-sadm-update %})             | How-to update to latest version of SADMIN   
| [sadmin.cfg]({% post_url 2021-04-26-sadmin-cfg %})                        | SADMIN main configuration file   
| [sadm_sysmon.pl]({% post_url 2021-06-10-sadm-sysmon %})                   | Client system monitor   
| [SysMon configuration file]({% post_url 2021-06-11-sadm-sysmon-config %}) | Client System Monitor configuration file     
| [smon]({% post_url 2021-06-15-sadm-sysmon-cli %})|   Allow you run SysMon and see the report file |   
| [How-to create a Slack workspace]({% post_url 2021-06-16-sadm-create-slack-workspace %}) | Create a Slack Workspace |  
| [How-to create Slack channel and App.]({% post_url 2021-06-17-sadm-create-slack-channel-and-slack-app %}) | Configure SADMIN to use Slack|  
| [How-to use SADMIN alerting system]({% post_url 2021-06-18-how-to-use-sadmin-alert %}) | Understanding SADMIN alerting system |  
| [Alert Group File]({% post_url 2021-06-19-alert-group-cfg %})                          | Alert group definition file |   
| [Slack channel file]({% post_url 2021-06-22-alert-slack-cfg %})                  |  Slack channel definition file |   




