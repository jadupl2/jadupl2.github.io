---
title:          How-to use SADMIN alerting system
permalink:      /how-to-use-sadmin-alert/
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
  - If you don't have one, you can read our [How-to create a Slack workspace]({% post_url 2021-06-16-sadm-create-slack-workspace %}) page and create one.
  - You will also need at least one channel and one Slack App in order to receive alert. If you don't, have a look at the [How-to create Slack channel and App]({% post_url 2021-06-17-sadm-create-slack-channel-and-slack-app %}) page.
- If you want to use the SMS method for alerting, see [How-to setup SMS notification](/how-to/how-to-sms) page before.
- If you want to use email alerting system, make sure you have valid email(s) address in the [SADMIN configuration file]({% post_url 2021-04-26-sadmin-cfg %}#sadm_mail_addr) .
- You'll need your favorite editor, to modify some configuration files and to create a test script.




### Understanding SADMIN alerting facilities
This guide, we will demonstrate with an example, how you can use the SADMIN alerting facilities.
{: .text-justify}



#### The default alert group

An alert can be issue in two ways, either by a script or by the SADMIN System Monitor. An alert 
is always sent to an alert group.
The **[default alert group name]({% post_url 2021-04-26-sadmin-cfg %}#sadm_alert_group)** used is 
the one specified in the SADMIN configuration file on the system that triggered the alert.
Every system have his own [SADMIN configuration file]({% post_url 2021-04-26-sadmin-cfg %}#sadm_alert_group) ($SADMIN/cfg/sadmin.cfg).
The default alert group after the installation is called (guess what) 'default'.
{: .text-justify}

```bash
#----------------------------------------------------------------------------
# Default Alert Group is 'default' (As defined in $SADMIN/cfg/alert_group.cfg)
# Group specified here, MUST exist in the $SADMIN/cfg/alert_group.cfg.
#
# Use in Script:
#   Default Alert Group use for sending alert within your script.
#   Default can be overridden by changing 'SADM_ALERT_GROUP' variable at the
#   top of the script.
#
# Use by System Monitor
#   When the System Monitor detect something that it could monitor (Like a
#   new filesystem), a new monitoring line is added with this Alert group.
#   Default can be overridden by changing the Warning Alert Group (Column J)
#   and the Error Alert Group (Column K), in the System Monitor configuration
#   file of the system ($SADMIN/cfg/`hostname -s`.smon).
#
#----------------------------------------------------------------------------
SADM_ALERT_GROUP = default
```


<br>
#### The default alert type

The alert type is use only at the end of the script, to decide if an alert/notification need to 
be send. The default alert type is set at installation time and is set to '1' (Alert only on error).
You can view the actual **[default alert type]({% post_url 2021-04-26-sadmin-cfg %}#sadm_alert_type)** 
by looking in the SADMIN configuration file ($SADMIN/cfg/sadmin.cfg). When you run a Python or a 
Shell script using the SADMIN Tools, it use this default value.
{: .text-justify}

```bash
#----------------------------------------------------------------------------
# Default option for sending alert (notification) after a SCRIPT terminate.
# This default, can be overridden by changing 'SADM_ALERT_TYPE' in the
# 'SADMIN code section' of your script.
# variable at the top of template script.
# 0 = Don't send any alert when script terminate.
# 1 = Send alert only if script terminate with error.
# 2 = Send alert only if script terminate with success.
# 3 = Always send notification with status when script terminate.
#----------------------------------------------------------------------------
SADM_ALERT_TYPE = 1
```

<dl>
<dt><b>The Alert type have four possible values :</b></dt>
<dd>0 Meaning that you don't want any alert to be send, either if the script finish with success or failure.</dd>
<dd>1 You want to send an alert only if the script finish with an error (Exit code not equal to 0).</dd>
<dd>2 An alert will be send only when the script finish with success (Exit code = 0).</dd>
<dd>3 Always send an alert, whether the script terminate with failure or success.</dd>
</dl>

[Back to the top](#top_of_page)




<br>
#### Overriding default alert group and alert type

You can override the default [alert group]({% post_url 2021-04-26-sadmin-cfg %}#sadm_alert_group) 
and [alert type]({% post_url 2021-04-26-sadmin-cfg %}#sadm_alert_type) by uncomment the variables 
SADM_ALERT_TYPE and/or SADM_ALERT_GROUP for shell script and st.cfg.alert_type and/or 
st.cfg_alert_group for Python value in the [SADMIN section]({% post_url 2021-05-07-sadmin-section %}) 
near the top of the script.
{: .text-justify}

**[Shell Script]({% post_url 2021-05-07-sadmin-section %}#description_shell)**

```bash
#export SADM_ALERT_TYPE=1            # 0=None 1=AlertOnErr 2=AlertOnOK 3=Always
#export SADM_ALERT_GROUP="default"   # AlertGroup Use for Alert(alert_group.cfg)
```

**[Python Script]({% post_url 2021-05-07-sadmin-section %}#description_python)**

```bash
#st.cfg_alert_type  = 1              # 0=None 1=AlertOnErr 2=AlertOnOK 3=Always
#st.cfg_alert_group = "default"      # AlertGroup use for Alert(alert_group.cfg)
```

[Back to the top](#top_of_page)
 



<br>
#### Overriding the default alert group in SADMIN System Monitor

The System Monitor alert group is specify in **column J for Warning** and in **column K for Error** 
of the [Sysmon configuration file]({% post_url 2021-06-11-sadm-sysmon-config %}). In the example 
below, we check filesystem "/opt" space usage. The filesystem usage is currently at 69%, the 
warning threshold is at 85% and the error at 90%.  

```bash
#Column 1  2  3  4  5   6   7    8   9 A B C D E F G    H       I     J      K   L
FS/opt     69 >= 85 90 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 sdevops sprod -
```

- If the filesystem usage percentage become greater or equal to 85%, a warning alert will be send to 'sdevops' alert group.
- If the filesystem usage percentage become greater or equal to 90%, an error alert will be send to 'sprod' alert group.
- If the Alert group used in SysMon configuration don't exist in the alert group file, the group 'default' is use.




<br>
#### Example of overriding default alert group and alert type in a script

The example that follow below is to show how to override the default alert group and alert type 
in your script. We will use the Slack alert method in this example.
{: .text-justify}

But before we begin, here is an example of the four different methods (m,t,c,s), you can use with
SADMIN.
{: .text-justify}

**Example of a typical alert group file**
```bash
# Email Alert Group 
e_sysadmin          m   batman@batcave.com
e_webteam           m   batman@batcave.com,robin@batcave.com

# SMS (Texto) Alert Group, members are Cellular name
sms_sysadmin        t   cell_support
sms_network         t   cell_support,cell_telecom
sms_emergency       t   cell_support,cell_telecom,cell_custsup

# Cellular number of individual (Use only in SMS alert group)
cell_support        c   5147577444
cell_telecom        c   5147560444
cell_custsup        c   4507570468
cell_support_1      c   4187779402
cell_support_2      c   5147779444

# Slack Alert Group
# 3th column is the channel name defined in Slack Alert file (alert_slack.cfg).
sdev                s   sadm_dev
sprod               s   sadm_prod
sinfo               s   sadm_info
sdevops             s   sadm_devops
```

The [alert group file]({% post_url 2021-06-19-alert-group-cfg %}) ($SADMIN/cfg/alert_group.cfg) 
below is the one we base our example upon.

![Alert Group File](/assets/img/sadm_alert/file_alert_group.png){: .align-center} 

Here is a portion of the Slack alert file ($SADMIN/cfg/alert_slack.cfg), we used for our example. 
![Slack Alert File](/assets/img/sadm_alert/file_alert_slack.png){: .align-center} 

Let's make a copy of the shell template script to create our test script.
In our test script, we will change the alert group from the default to 'sprod' and the alert type from 1 to 3.
Let's begin by typing the following command to create our test script name 'sadm_test_alert.sh' ;

```bash
# cd $SADMIN/usr/bin
# /sadmin/usr/bin  
# /sadmin/usr/bin cp $SADMIN/bin/sadm_template.sh sadm_test_alert.sh
# /sadmin/usr/bin nano sadm_test_alert.sh
```

With your favorite editor change the circled lines.

**Script before the change**
![Script before change](/assets/img/sadm_alert/test_alert_before05.png){: .align-center} 


**Script after the change**
![Script after change](/assets/img/sadm_alert/test_alert_after_10.png){: .align-center} 

**Running our test script**
![Run test script](/assets/img/sadm_alert/test_alert_screen_output.png){: .align-center} 

**Alert that we received in Slack**
![Slack Alert received](/assets/img/sadm_alert/test_alert_slack_alert.png){: .align-center} 

**A look at the 'log' and 'rch' file generated**
![Log and rch generated](/assets/img/sadm_alert/test_alert_rch_and_log.png){: .align-center} 

It is simple as that, so I hope you have a better understanding of how the alarm system work in SADMIN.
We could have done the same test using the Python template ($SADMIN/bin/sadm_template.py) script. 
{: .text-justify}




<br>
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
| [How-to create a Slack workspace]({% post_url 2021-06-16-sadm-create-slack-workspace %}) | Create a Slack Workspace |    
| [How-to create Slack channel and App.]({% post_url 2021-06-17-sadm-create-slack-channel-and-slack-app %}) | Configure Slack Channel |   
| [How-to use SADMIN alerting system]({% post_url 2021-06-18-how-to-use-sadmin-alert %}) | Understanding SADMIN alerting system |  

