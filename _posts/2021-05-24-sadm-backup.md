---
title:          sadm_backup.sh
permalink:      /sadm-backup/ 
desc:           Daily backup based on the content of the backup list & exclude file
version:        3.29
updated:        2021-07-26
os:             Linux
type:           B  # [D]oc [S]=Server only [C]=Client [B]oth
tags:           [ backup ] 
categories:     [ backup ] 
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
{% include sadm/sadm_page_info.md %}


<a id="name"></a>
## NAME
**{{ page.title }}** - *{{ page.desc }}*   



<a id="synopsis"></a>
## SYNOPSIS

```bash
{{ page.title }} [-d 0-9] [-h] [-n] [-v]
```
{% if page.type == "S" %}
<font size="3"><strong>Can only be run on SADMIN Server.</strong></font>
{% endif %}
{% if page.type == "B" %}
<font size="3"><strong>Can be executed on a client and on the SADMIN Server.</strong></font>
{% endif %}


<a id="description"></a>
## DESCRIPTION

This script is use to create backups (tar or tgz) of directories and files you specify on the web
interface. 


<a id="backup_schedule"></a>
## Create a backup schedule

To access the "Daily backup schedule" web page, click on "Daily Backup" in the located in the 
heading portion of the web site. You will then be presented with a list of your systems, just click
on a server name and you'll be redirected to "Daily backup schedule" page of the system.
{: .text-justify}
![Daily Backup Page Access](/assets/img/sadm_backup/sadm_daily_backup.png){: .align-center}

You will then be presented with a list of your systems, just click on the server name and you be 
redirected to "Daily backup schedule" page of the system.
{: .text-justify}
![Daily Script Backup](/assets/img/sadm_backup/sadm_backup_web_screen.png){: .align-center}

This backup script is automatically run by the backup crontab (/etc/cron.d/sadm_backup), if the "System 
Status" is set to "Active" on the system maintenance page and the "Activate Backup" is set to "yes" 
on the daily backup schedule web page. On the "Daily backup schedule" page, you also need to 
specify the time you want to do the backup. If the "Activate Backup" is set to "no", obviously 
no backup will be schedule for the system. You can also run this script manually `"sadm_backup.sh"` 
whenever you want to create a new backup.
{: .text-justify}
![Activate Backup](/assets/img/sadm_backup/sadm_backup_web_activate.png){: .align-center}

There are two text areas where you specify the files and directories you want to backup and the one 
you want to exclude. You may want to backup the "/home" directory, but not the "Downloads" directory
of user "jacques", then you would add a line like this one "./home/jacques/Downloads" in the exclude 
list text area.
{: .text-justify}

### The Backup List
The directories and files you specify in the "Backup List (Files & Dir.)" text-area are written
to a file called the "backup list" ($SADMIN/cfg/backup_list.txt). If the backup list file is not 
present when the script is started, a default backup list file ($SADMIN/cfg/.backup_list.txt) 
is use as a starting backup list. Specify the full path for each directories and files you want 
to backup. For every directory (or file) specified in the backup list, a backup file will be 
produced along with a log of the backup. For example, if you specify '/home' and '/etc' in the 
backup list, four backup files will be produced, one file the 'home' directory and one for the 'etc' 
directory and each of them will have a log (See directory structure below). The log can be viewed
in case of error or if you are not sure of what is in the backup file.
When you modify the backup list for a system it is written locally to a temporary file 
"$SADMIN/www/dat/HOSTNAME/cfg/backup_list.tmp" and it's transferred to the proper system the next
time "[sadm_fetch_clients.sh]({% post_url 2021-03-16-sadm-fetch-clients %})" script is run, so your 
change could not take up to 5 minutes to get to the proper system.
{: .text-justify}

**Example of a backup list**

```bash
# v1.5 Initial Backup List - template
# Notes: Socket Files are automatically excluded
# One file or directory per line
# -----------------------------------------------
#
$SADMIN
/home 
/etc 
/root
/var
```


<!-- ![Daily Backup List](/assets/img/sadm_backup/sadm_backup_backup_list.png){: .align-center}  -->

Directories and files specified in the backup list that cannot be found during backup execution 
are skipped and identified as such in the log file and are not consider as an error, but as warning. 
This give you the flexibility to use the same backup_list.txt file across multiple servers.  
{: .text-justify}
![Backup Dir Not Found](/assets/img/sadm_backup/sadm_backup_notfound.png){: .align-center}

### The Exclude List
The directories and files you specify in the "Exclude List" text-area are written to a file called 
the backup exclude file ($SADMIN/cfg/backup_exclude.txt) and are excluded from the backup. If the 
backup exclude file is not present when the script is started, the default exclude file 
($SADMIN/cfg/.backup_exclude.txt) is use as the exclude list. Notice, that lines from file are read 
verbatim. One of the frequent errors is leaving some extra whitespace after a file name, which is 
difficult to catch using text editors. However, empty lines are OK. Trailing slashes at the end of 
excluded folders will cause tar to not exclude those folders at all.
{: .text-justify}

**Please note:** 
Before starting the backup (tar command), the script do a "cd /" to be positioned
at the root of the system. The directory or file specified are prefixed by './', so the backup 
content can be restore in a directory of your choice. 
 {: .notice--info} 
 
When you modify the backup exclude list for a system it is written to a local temporary file 
"$SADMIN/www/dat/HOSTNAME/cfg/backup_exclude.tmp" and it's transferred to the proper system the next
time "[sadm_fetch_clients.sh]({% post_url 2021-03-16-sadm-fetch-clients %})" script is run, so your 
change could take up to 5 minutes to get to the proper system.
{: .text-justify}

**Example of an exclude list**
```bash
# V1.6 Initial Exclude List 
# Files extensions to exclude
*.iso 
*.pyc

# Files to exclude
sysmon.lock 

# Directories to exclude
__pycache__

# Exclude content of these directories
*/tmp/*
*/Trash/*
*/Downloads/*
*/tmp/*
*/Trash/*
#
```

<!-- ![Backup Exclude List](/assets/img/sadm_backup/sadm_backup_exclude.png){: .align-center}  -->


### Backup preservation policies 
The backup files are stored on the NFS server specified in $SADMIN/cfg/sadmin.cfg (see example 
below). In the example below, the backup is stored on the NFS server name "batnas.maison.ca" in the
directory "/volume1/backup_linux". By default, 4 copies of the daily backup will be kept, but you 
can modify this choice by changing the field "SADM_DAILY_BACKUP_TO_KEEP" in SADMIN configuration 
file "[$SADMIN/cfg/samin.cfg]({% post_url 2021-04-26-sadmin-cfg %})". The remaining parameters, I 
think are self explanatory. Extra backup are deleted at the end of each backup. 
{: .text-justify}

![Backup parameters in sadmin.cfg](/assets/img/sadm_backup/sadm_backup_cfg.png){: .align-center}

[Back to the top](#top_of_page)



<a id="examples"></a>
## EXAMPLE
This is an example of the output you get when you run the {{ page.title }} manually. This script 
must be run by the 'root' user to have access to all directory to backup and mount the NFS drive.
```bash
rroot@yoda:~  # sadm_backup.sh
================================================================================
Tue May 25 10:06:12 AM EDT 2021 - sadm_backup.sh V3.30 - SADM Lib. V3.70
Server Name: yoda.maison.ca - Type: LINUX
FEDORA 34 Kernel 5.11.11-200.fc33.x86_64
==================================================
 
Mounting NFS Drive on batnas.maison.ca.
mount batnas.maison.ca:/volume1/backup_linux /mnt/backup
[SUCCESS] NFS Mount Succeeded.

Setup Backup Environment ...
Removing previous backup links in /mnt/backup/yoda/latest 
Making today backup directory /mnt/backup/yoda/daily/2021_05_25 
 
Today Tue May 25 10:06:12 AM EDT 2021 we are starting a [Daily] backup ...
 
Base on SADMIN configuration file, you have chosen to:
 - Keep 4 daily backups
 - Keep 4 weekly backups
 - Keep 3 monthly backups
 - Keep 2 yearly backups
 - Do the weekly backup on Friday
 - Do the monthly backup on the 1 of every month
 - Do the yearly backup on the 31 of December every year
 - Backup directory is /mnt/backup/yoda/daily/2021_05_25
 - Using backup list file /opt/sadmin/cfg/backup_list.txt
 - Using backup exclude list file /opt/sadmin/cfg/backup_exclude.txt
 
----------
Current directory: [/opt/sadmin]
tar -cvzf /mnt/backup/yoda/daily/2021_05_25/2021_05_25-10_06_13_opt_sadmin.tgz -X /tmp/exclude .
Create Link to latest backup of /opt/sadmin in /mnt/backup/yoda/latest
[SUCCESS] Creating Backup 2021_05_25-10_06_13_opt_sadmin.tgz
 
----------
Current directory: [/home]
tar -cvzf /mnt/backup/yoda/daily/2021_05_25/2021_05_25-10_06_30_home.tgz -X /tmp/exclude .
Create Link to latest backup of /home in /mnt/backup/yoda/latest
[SUCCESS] Creating Backup 2021_05_25-10_06_30_home.tgz
 
----------
Current directory: [/etc]
tar -cvzf /mnt/backup/yoda/daily/2021_05_25/2021_05_25-10_07_24_etc.tgz -X /tmp/exclude .
Create Link to latest backup of /etc in /mnt/backup/yoda/latest
[SUCCESS] Creating Backup 2021_05_25-10_07_24_etc.tgz
 
----------
Current directory: [/root]
tar -cvzf /mnt/backup/yoda/daily/2021_05_25/2021_05_25-10_07_27_root.tgz -X /tmp/exclude .
Create Link to latest backup of /root in /mnt/backup/yoda/latest
[SUCCESS] Creating Backup 2021_05_25-10_07_27_root.tgz
 
----------
Current directory: [/var]
tar -cvzf /mnt/backup/yoda/daily/2021_05_25/2021_05_25-10_07_28_var.tgz -X /tmp/exclude .
Create Link to latest backup of /var in /mnt/backup/yoda/latest
[SUCCESS] Creating Backup 2021_05_25-10_07_28_var.tgz

----------
Backup file: /example/somefile
[ WARNING ] [/example/somefile] doesn't exist on yoda

----------
Backup file: /somedir
[ WARNING ] [/somedir] doesn't exist on yoda
 
----------
 
Total error(s) while creating backup: 0.

Content of today backup directory (/mnt/backup/yoda/daily/2021_05_25):
total 961960
-rw-rw-r--. 1 nobody users     21549 May 25 10:06 2021_05_25-10_06_13_opt_sadmin.log
-rw-rw-r--. 1 nobody users 162715212 May 25 10:06 2021_05_25-10_06_13_opt_sadmin.tgz
-rw-rw-r--. 1 nobody users   2476587 May 25 10:07 2021_05_25-10_06_30_home.log
-rw-rw-r--. 1 nobody users 397883167 May 25 10:07 2021_05_25-10_06_30_home.tgz
-rw-rw-r--. 1 nobody users     89741 May 25 10:07 2021_05_25-10_07_24_etc.log
-rw-rw-r--. 1 nobody users   6190273 May 25 10:07 2021_05_25-10_07_24_etc.tgz
-rw-rw-r--. 1 nobody users      2165 May 25 10:07 2021_05_25-10_07_27_root.log
-rw-rw-r--. 1 nobody users    801965 May 25 10:07 2021_05_25-10_07_27_root.tgz
-rw-rw-r--. 1 nobody users    184918 May 25 10:09 2021_05_25-10_07_28_var.log
-rw-rw-r--. 1 nobody users 414648217 May 25 10:09 2021_05_25-10_07_28_var.tgz


Applying chosen retention policy to /mnt/backup/yoda/daily directory
List of backup currently on disk:
2021_05_25
2021_05_23
2021_05_22
2021_05_20

Keep only the last 4 days of each backup.
We now have 4 days of backup(s).
No clean up needed

Unmounting NFS mount directory /mnt/backup.
[SUCCESS] Unmounting NFS Dir. /mnt/backup

==================================================
Script exit code is 0 (Success) and execution time is 00:03:52
History (/opt/sadmin/dat/rch/yoda_sadm_backup.rch) trim to 35 lines ($SADM_MAX_RCLINE=35).
Script will send an alert only when it terminate with error ($SADM_ALERT_TYPE=1).
Script succeeded, no alert will be send to 'default' alert group.
New log (/opt/sadmin/log/yoda_sadm_backup.log) created ($SADM_LOG_APPEND='N').
End of sadm_backup.sh - Tue May 25 10:09:54 AM EDT 2021
================================================================================
```

## Backup directory structure

Directory structure in which the backup are stored offer the flexibility needed to quickly access 
to your backup in case you need them. Each system have a dedicated directory, named by is hostname.
In each host directory there is a 'daily', 'weekly', 'monthly', 'yearly' and a 'latest' directory.
When a backup is done, a new sub-directory is created with the current date. So it is easy to find 
the backup you need. If you are looking for the latest backup of a server, go in the host 
sub-directory and then in the 'latest' sub-directory, the more recent backup will always be there.
After a couple of months, the backup directories structure should look similar to the one below.  
**For example, let's look at the backup structure :**
{: .text-justify}

```bash
# pwd
/volume1/backup_linux/yoda
# find . -type d 
.
./daily
./daily/2021_05_22
./daily/2021_05_23
./daily/2021_05_24
./daily/2021_05_20
./weekly
./weekly/2021_05_21
./weekly/2021_05_14
./weekly/2021_04_23
./weekly/2021_05_07
./monthly
./monthly/2021_02_01
./monthly/2021_03_01
./monthly/2021_04_01
./monthly/2021_01_01
./yearly
./yearly/2020_12_31
./latest
#
```

[Back to the top](#top_of_page)

{% include {{ site.section_options     }} %}
| **-n** | Do NOT compress backup | 

{% include {{ site.section_environment }} %}

{% include {{ site.section_exitcode    }} %}

{% include {{ site.section_author      }} %}

{% include {{ site.section_copyright   }} %}


<a id="seealso"></a>
## SEE ALSO
[sadmin.cfg]({% post_url 2021-04-26-sadmin-cfg %}) - SADMIN main configuration file  
[sadm_fetch_clients.sh]({% post_url 2021-03-16-sadm-fetch-clients %}) - rsync all .rch/.log/.rpt from actives clients to the SADMIN server.  
