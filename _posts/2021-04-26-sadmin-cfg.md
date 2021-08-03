---
title:          sadmin.cfg
permalink:      /sadmin-cfg/
desc:           SADMIN configuration file.
version:        2.4
updated:        2021-04-26
os:             Linux, Aix, MacOS
type:           D  # [D]oc [S]=Server only [C]=Client [B]oth
layout:         single
search:         true
tags:           [ configuration_files ] 
categories:     [ configuration_files ] 
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

<font size="3">
<div>$SADMIN/cfg/{{ page.title }} - v{{ page.version }}</div>  
<div>Posted {{ page.date | date: "%Y-%m-%d" }} - Updated {{ page.updated }}</div>  
<div>Supported on {{ page.os }}</div>  
</font>  
  

## Format of the SADMIN configuration file

Comment line MUST begin with an # in column 1 and blank line are ignored. The format is simple 
"NAME = VALUE", NAME must start in column 1. The 'VALUE' is initially set by the setup script 
during installation, but some of them can be changed on a script basis. Fields like 
'[SADM_ALERT_TYPE]({% post_url 2021-04-26-sadmin-cfg %}#sadm_alert_type)' and 
'[SADM_MAIL_ADDR]({% post_url 2021-04-26-sadmin-cfg %}#sadm_mail_addr)' can be overridden in the 
[SADMIN section of the script]({% post_url 2021-05-07-sadmin-section %}#sadmin_shell_section). 
See the templates, '[sadm_template.sh]({% post_url 2021-03-16-sadm-template-sh %})' 
and '[sadm_template-py]({% post_url 2021-03-16-sadm-template-py %})' as examples.
{: .notice--warning}

If SADMIN main configuration file ($SADMIN/cfg/sadmin.cfg) is not present when the first script 
is run, then template file '**.sadmin.cfg**' will be copied to '**sadmin.cfg**'. If both file 
'sadmin.cfg' and '.sadmin.cfg' are not present default values are used.
 {: .notice--info} 


<a id="sadm_host_type"></a>
## The SADMIN Host Type
```bash
#----------------------------------------------------------------------------
# This field indicate whether this host is a SADMIN [S]erver or a [C]lient.
# It's used in various script to activate/deactivate some feature/operation.
# Set this field accordingly, there can be only one SADMIN Server
# Valid value are : [S]erver, [C]lient, [D]evelopment
# [D]evelopment Host Type is not used at the moment.
#----------------------------------------------------------------------------
SADM_HOST_TYPE = S
```



<a id="sadm_cie_name"></a>
## The name of your company (or site)
```bash
#----------------------------------------------------------------------------
# This is your company name (or site name) that will appear in the heading 
# of the web site and on some report and email that SADMIN produce.
#----------------------------------------------------------------------------
SADM_CIE_NAME = Your Cie Name
```



<a id="sadm_mail_addr"></a>
## The SADMIN administrator(s) email(s)
```bash
#----------------------------------------------------------------------------
# This field specify the email address used by SADMIN Tools to send various 
# email. For example, you can request that the log of a script be sent when 
# an error occurred or every time is it run. (See SADM_ALERT_TYPE later on)
# Multiple email can be specify, a comma must separate each of them.
#----------------------------------------------------------------------------
SADM_MAIL_ADDR = batman@batcave.com,robin@batcave.com
```



<a id="sadm_alert_type"></a>
## The default alert type
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


<a id="sadm_alert_group"></a>
## The default alert group

Related information about the alert group :   
- [Setting the default alert group]({% post_url 2021-03-16-how-to-sms %}#setting-default-alerting-group).  
- [Changing the default alert group]({% post_url 2021-03-16-how-to-sms %}#changing-the-default-alerting-group).  
- [Overriding default alert group in a script]({% post_url 2021-03-16-how-to-sms %}#override-the-default-alert-group-and-type-in-a-script).  
- [Overriding default alert group in SADMIN System Monitor]({% post_url 2021-03-16-how-to-sms %}#override-default-alert-group-in-sadmin-system-monitor)  

```bash 
#----------------------------------------------------------------------------
# The SADMIN alert group are defined in '$SADMIN/cfg/alert_group.cfg' file.
# The default alert group is named 'default'.
# The group name specified here, MUST exist in the alert group file.
#
# Use in Script: 
#   - Default Alert Group name is use for sending alert within your script.
#   - The alert group name can be overridden by changing 'SADM_ALERT_GROUP' 
#     variable in the 'SADMIN code section'.
#
# Use by System Monitor:
#   - When the System Monitor detect something that it could monitor (Like a 
#     new filesystem), a new monitoring line is added with this Alert group.
#   - You can override the default define below by changing the Warning 
#     Alert Group (Column J) and the Error Alert Group (Column K), in the 
#     System Monitor configuration file of the system 
#     ($SADMIN/cfg/`hostname -s`.smon).
#
#----------------------------------------------------------------------------
SADM_ALERT_GROUP = default
```



<a id="sadm_textbelt"></a>
## The TextBelt Key for sending SMS alert
For more information on TextBelt setup, see the [How-to use SMS/Texto alerting system]({% post_url 2021-03-16-how-to-sms %}) page.
```bash
#----------------------------------------------------------------------------
# TEXTBELT SMS TEXT MESSAGE VARIABLE
# This is the key generated by TextBelt and the URL to use the SMS Service
# Go to https://textbelt.com/ and press the 'Generate my key' button.
# Enter your email address and decide what is the right plan for you.
# It's $10 for 250 Text Messages, $20 for 600, $40 for 1200.
#----------------------------------------------------------------------------
SADM_TEXTBELT_KEY = 967e5a9315d22dddd8f33a5b645ab0a855900f042NFZPGjohx1JnCrjsd64hd52k9
SADM_TEXTBELT_URL = https://textbelt.com/text
```


<a id="sadm_alert_repeat"></a>
## Number of seconds before repeating an alert (On same Day)
```bash
#----------------------------------------------------------------------------
# Default is 0 - Alerted once for the same alert.
#
# The "SADM_ALERT_REPEAT" variable is the number of seconds to wait before 
# the same alert is sent again within the same day. This number can range 
# from 0 to 85800 ((86400=24Hrs)-(600=10Min))=85800). For example, if you 
# set this variable to 43200 seconds, it means that if event of the alert 
# is not solve in the next 12hrs, an alert will be sent again after 12hrs
# (43200 Sec.) and this will be the last one. Script alert older that 24Hrs 
# are skipped and do not generate an alert.
#
# For System monitor Alert: 
# If the problem is not solved the next day, a new alert is sent 
# approximately at the same time the first one was.
# If you don't want the alert to repeat the next day, you need to :
#  - Correct the problem or change the test line in `hostname.smon` file.
#
# For Script Alert:
# To correct the problem, you need to re-run the script or change the 
# Result Code to '0' in (RCH) on the last column of the last line in the 
# corresponding rch file.
#----------------------------------------------------------------------------
SADM_ALERT_REPEAT = 0
```



<a id="sadm_server"></a>
## The SADMIN server name

```bash
#----------------------------------------------------------------------------
# SADMIN Server - (MUST be fully qualified name)
# This name MUST NOT be an alias in the DNS
# It MUST be the result of the 'hostname' command on the SADMIN server
#----------------------------------------------------------------------------
SADM_SERVER = holmes.maison.ca
```




<a id="sadm_ssh_port"></a>
## The SSH port number used to communicate with SADMIN clients.
This value can be changed on a script basis, by changing the value of the variable "$SADM_SSH_CMD"
at the end of the 'SADMIN code section' in your script.
{: .text-justify}

```bash
#----------------------------------------------------------------------------
# Standard Port for SSH is 22 - But if you use a different port put it here
#----------------------------------------------------------------------------
SADM_SSH_PORT = 32
```





<a id="sadm_rrdtool"></a>
## The location of the rrdtool command

```bash
#----------------------------------------------------------------------------
# Location of the rrdtool binary (Round Robin Database Tool)
# Used to record and produce performance statistics.
#----------------------------------------------------------------------------
SADM_RRDTOOL = /bin/rrdtool
```




<a id="sadm_domain"></a>
## The SADMIN Domain name
This is the default domain used when we add a new client to the SADMIN Tools via the web interface.

```bash
#----------------------------------------------------------------------------
# Default Domain when adding new server to SADMIN Tools
#----------------------------------------------------------------------------
SADM_DOMAIN = maison.ca
```




<a id="sadm_user"></a>
## SADMIN default user and group name

```bash
#----------------------------------------------------------------------------
# This is the user and group that have access to $SADM_BASE_DIR (/sadmin)
# sadm_housekeeping_client.sh and sadm_housekeeping_server.sh will use them
# to make sure all files and directories belong to them. 
#----------------------------------------------------------------------------
SADM_USER = sadmin
SADM_GROUP = sadmin
```


<a id="sadm_www_user"></a>
## Apache user and group name

```bash
#----------------------------------------------------------------------------
# This is the user and group that run the apache server. 
# Do a 'ps -ef | grep -Ei "httpd|apacahe2"' & look at the name in column one,
# for the user name (SADM_WWW_USER).
# And give the same name to the group name (SADM_WWW_GROUP).
# sadm_housekeeping_server.sh will use them to make sure all files and
# directories belong to them.
# They should be set to the user and group that is running the http server.
# On RedHat/CentOS/Fedora it is usually apache/apache
# On Ubuntu/Debian/Raspbian,LinuxMint it is usually www-data/www-data
#----------------------------------------------------------------------------
SADM_WWW_USER  = apache
SADM_WWW_GROUP = apache
```




<a id="sadm_dbname"></a>
## SADMIN Database information

```bash
#----------------------------------------------------------------------------
# MARIADB/MYSQL DATABASE PARAMETERS
#----------------------------------------------------------------------------
SADM_DBNAME     = sadmin
SADM_DBHOST     = sadmin.maison.ca
SADM_DBPORT     = 3306
SADM_RW_DBUSER  = rw_password
SADM_RO_DBUSER  = ro_password
```


<a id="sadm_max_logline"></a>
## Controlling log file size

```bash
#----------------------------------------------------------------------------
# SADM_MAX_LOGLINE is the maximum number of lines that each log can have.
#   - The default value is 500 lines.
#   - The Log filename is  "[HOSTNAME]_sadm_[NAME_OF_SCRIPT].log"
#   - They are located in ${SADMIN}/log directory.
#   - Log are created/updated automatically when you use the SADMIN Library.
#   - Log are automatically trimmed to this number at the end of the script.
#   - By Default the value below will is use.
#   - If you want a different value, change the line below in your script.
#
# In Shell Script:
#   export SADM_MAX_LOGLINE = 500  # When Script End Trim log to 500 Lines
#
# In Python Script:
#   instance.cfg_max_logline = 500 # When Script End Trim log to 500 Lines
#
#----------------------------------------------------------------------------
SADM_MAX_LOGLINE = 500
```




<a id="sadm_max_rchline"></a>
## Controlling RCH (Result Code History) file size

```bash
#----------------------------------------------------------------------------
# SADM_MAX_RCHLINE is the maximum number of lines that '*.rch' file can have.
#   - [R]esult [C]ode [H]istory file, record script execution history.
#   - The RCH filename are "[HOSTNAME]_sadm_[NAME_OF_SCRIPT].rch"
#   - They are located in ${SADMIN}/dat/rch directory.
#   - RCH file are automatically trimmed to this number when script end.
#   - RCH file are created/updated each time the script start and end.
#   - By Default the value below will is use.
#   - If you want a different value in a script, you can do the following ;
#
# In Shell Script:
#   export SADM_MAX_RCHLINE  = 35  # When Script End Trim log to 35 Lines
#
# In Python Script:
#   instance.cfg_max_rchline = 35  # When Script End Trim log to 35 Lines
#
#   If you wish not to use the RCH file in one of your script 
#   (Interactive Script for Example). 
#   Then you would change the variable below in the SADMIN Code Section.
#
# In Shell Script : 
#   export SADM_USE_RCH="N"         # Don't generate entry in RCH file
#
# In Python Script : 
#   Instance.use_rch = False        # Don't generate entry in RCH file
#----------------------------------------------------------------------------
SADM_MAX_RCHLINE = 35
```


<a id="sadm_nmon_keepdays"></a>
## Performance monitor files (*.nmon) retention period
```bash
#----------------------------------------------------------------------------
# SADM_NMON_KEEPDAYS is the number of days we want to keep a nmon file in
# $SADMIN/dat/nmon directory.
#
#   - The "sadm_housekeeping_client.sh" script run automatically every day
#     and delete any nmon files older that the number of days specified.
#   - Default value of 60 days, is a reasonable default (each file is 500k).
#
# NMON file is an ASCII file created by the 'nmon' program that store system
# performance data. Normally one NMON file is produced daily by each system.
#   - NMON file are recorded in $SADMIN/dat/nmon directory.
#   - The name of each nmon file is "[HOSTNAME]_[yymmdd]_[hhmm].nmon"
#   - The Home page of nmon is http://nmon.sourceforge.net/pmwiki.php
#   - SADMIN setup script will install 'nmon' if not present on your system,
#     but it is usually include in the distribution repository.
#   - You can find a copy of nmon for your env. in ${SADMIN}/pkg/nmon dir.
#   - SADM Tool use nmon file to record performance data in RRD File.
# -----
# Once a day the nmon directory ($SADMIN/dat/nmon) of each clients is sync 
# (rsync) to the SADMIN server. 
# This is done daily by the "sadm_server_sunrise.sh" script that run early 
# in the morning (etc/cron.d/sadm_server).
# At midnight the current nmon file is closed and a new one created.
#----------------------------------------------------------------------------
SADM_NMON_KEEPDAYS = 40
```



<a id="sadm_rch_keepdays"></a>
## Result Code History files (*.rch) retention period
Define how many days to keep an unmodified RCH file.

```bash
#----------------------------------------------------------------------------
# Variable SADM_RCH_KEEPDAYS indicated the number of days we wait, until we
# deleted a RCH file that was not updated for the number of days specified.
#
# - The RCH files are located in ${SADMIN}/dat/rch directory.
# - We don't want an unused/oudated RCH file to stay there for ever.
#
# If an RCH is not updated for a long time, this may indicate that the 
# associated script don't exist anymore or as not been run for a while. 
#
# - Recommended value is 40 days.
# - A value of zero, means you don't want to delete any of the rch logs.
# - It's the "sadm_client_housekeeping.sh" that is responsible to delete the
#   rch, if necessary. It's part of the "${SADMIN}/bin/sadm_client_sunset.sh"
#   that is executed from the /etc/cron.d/sadm_client crontab every night.
#----------------------------------------------------------------------------
SADM_RCH_KEEPDAYS = 40
```



<a id="sadm_log_keepdays"></a>
## Log files (*.log) retention period
Define how many days to keep an unmodified log.

```bash
#----------------------------------------------------------------------------
# The LOG files are located in ${SADMIN}/log directory.
# The LOG files are updated every time the associate script is run.
#
# If an LOG is not updated for a long time, this may indicate that the
# associated script don't exist anymore and as not been run for a while.
# If we don't do anything, the LOG file will may stay there for ever.
#
# The variable SADM_LOG_KEEPDAYS indicated the number of days we wait, until 
# we deleted a LOG file that was not updated for the number of days specified.
#
# - Recommended value is 40 days.
# - A value of zero, means you don't want to delete any of the old logs.
# - It's the "sadm_client_housekeeping.sh" that is responsible to delete the
#   logs if necessary. It's part of the "${SADMIN}/bin/sadm_client_sunset.sh"
#   that is executed from the /etc/cron.d/sadm_client crontab every night.
#----------------------------------------------------------------------------
SADM_LOG_KEEPDAYS = 40
```




<a id="sadm_rear_nfs_server"></a>
## ReaR backup information
The information below indicate the NFS server and mount point to store the ReaR backup image and
how many copy we want to keep.

```bash
#----------------------------------------------------------------------------
# NFS Server name where the Rear Backup are Stored
# NFS mount point where the Rear Backup are stored on the NFS Server
# Number of Rear Backup to keep at all time.
#----------------------------------------------------------------------------
SADM_REAR_NFS_SERVER        = batnas.maison.ca
SADM_REAR_NFS_MOUNT_POINT   = /volume1/backup_rear
SADM_REAR_BACKUP_TO_KEEP    = 3
```




<a id="sadm_backup_nfs_server"></a>
## Daily backup Information
Information below indicate where the daily backup will be stored, when the type of backup is done 
and defined the retention policy for each type of backup. This information is used by the 
"sadm_backup.sh" script.
{: .text-justify}

```bash
#----------------------------------------------------------------------------
# Backup Script (sadm_backup.sh) to NFS or Local mount point
#----------------------------------------------------------------------------
SADM_BACKUP_NFS_SERVER      = batnas.maison.ca
SADM_BACKUP_NFS_MOUNT_POINT = /volume1/backup_linux

# Number of days to keep each type of backup
SADM_DAILY_BACKUP_TO_KEEP   =   4
SADM_WEEKLY_BACKUP_TO_KEEP  =   4
SADM_MONTHLY_BACKUP_TO_KEEP =   3
SADM_YEARLY_BACKUP_TO_KEEP  =   2

# Define what day to do a weekly backup 
# 1=Mon, 2=Tue, 3=Wed, 4=Thu, 5=Fri, 6=Sat, 7=Sun
SADM_WEEKLY_BACKUP_DAY      =   5     

# Define the date of the month to do a Monthly Backup
# Same date for every month.
# So should be between the 1st and the 28th.
SADM_MONTHLY_BACKUP_DATE    =   1    

# Define the Month and Date When to do a Yearly Backup
SADM_YEARLY_BACKUP_MONTH    =   12
SADM_YEARLY_BACKUP_DATE     =   31
```



<a id="sadm_mksysb_nfs_server"></a>
## AIX mksysb information
Below is the information that indicate where the AIX mksysb image will be stored and what is the
retention policy (Used by sadm_create_mksysb.sh script).
 ```bash
#----------------------------------------------------------------------------
# NFS Server, mount point and Number of Mksysb backup to keep 
#----------------------------------------------------------------------------
SADM_MKSYSB_NFS_SERVER      = batnas.maison.ca
SADM_MKSYSB_NFS_MOUNT_POINT = /volume1/mksysb
SADM_MKSYSB_BACKUP_TO_KEEP  = 2
```



<a id="sadm_network"></a>
## The network subnet you want to scan every day
You can define up to five subnets to scan every day. This information is used by the network 
scanning script "sadm_subnet_lookup.py", which is executed by "sadm_server_sunrise.sh" every 
morning from the SADMIN server crontab file "/etc/cron.d/sadm_server".
{: .text-justify}
```bash
#----------------------------------------------------------------------------
# Network that we want to scan daily and have HostName Discover (DNS)
# and Mac Address
#----------------------------------------------------------------------------
SADM_NETWORK1 = 192.168.1.0/24
SADM_NETWORK2 = 
SADM_NETWORK3 =
SADM_NETWORK4 =
SADM_NETWORK5 =
```

