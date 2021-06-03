---
title:          sadm_backupdb.sh
desc:           Backup one or all MySQL/MariaDB Databases present on the system
version:        3.29
updated:        2021-05-26
os:             Linux
type:           S  # [D]oc [S]=Server only [C]=Client [B]oth
tags:           [ server-scripts ] 
categories:     [ server-scripts ] 
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
{{ page.title }} [-b backup_dir] [-d 0-9] [-h] [-n dbname] [-u] [-v]
```
{% if page.type == "S" %}
<font size="3"><strong>Can only be run on SADMIN Server.</strong></font>
{% endif %}
{% if page.type == "B" %}
<font size="3"><strong>Can be executed on a client and on the SADMIN Server.</strong></font>
{% endif %}


<a id="description"></a>
## DESCRIPTION

The function of this script is to take a backup of our SADMIN database, but by default it take a 
backup of all databases present on the SADMIN server into the "$SADMIN/dat/dbb" directory. If you 
want to backup only one database, you can use the '-n' command line options and specify the name 
of the database to backup. 
This backup is run automatically by the "[sadm_server-sunrise.sh]({% post_url 2021-05-26-sadm-server-sunrise %})" script early every morning via 
SADMIN server crontab (/etc/cron.d/sadm_server).
{: .text-justify}

The file name follow this pattern "databaseName_YYYY_MM_DD_HH_MM_SS.sql.gz". For example, "sadmin_2018_07_13_05_46_25_Friday.sql.gz" is the backup file for the 'sadmin' database 
taken at 05:46:25AM on July the 13th 2018. The default backup directory structure where the backup 
is created is "${SADMIN}/dat/dbb", but you can specify the backup directory of your choice with the
 '-b' command line option. In the backup directory, backup are group by type: 'daily','weekly',
 'monthly','yearly' and the 'latest' directory. In each of these directories, there is a 
sub-directory for each of the database that's backup. If you're looking for the latest Database 
backup, go in the 'latest' sub-directory, the more recent backup will always be there. After a 
couple of months, the backup directory structure should look similar to the one below.  
{: .text-justify}

**After a couple of months, the backup directory structure should look similar to this:**  
```bash
$ cd $SADMIN/dat/dbb
/sadmin/dat/dbb $ find . | grep sadmin
./daily/sadmin
./daily/sadmin/sadmin_2021_05_25_13_05_06_Tuesday.sql.gz
./daily/sadmin/sadmin_2021_05_26_13_09_54_Wednesday.sql.gz
./daily/sadmin/sadmin_2021_05_27_05_38_21_Thursday.sql.gz
./daily/sadmin/sadmin_2021_05_29_05_50_39_Saturday.sql.gz
./weekly/sadmin
./weekly/sadmin/sadmin_2021_05_07_05_38_14_Friday.sql.gz
./weekly/sadmin/sadmin_2021_05_14_05_38_19_Friday.sql.gz
./weekly/sadmin/sadmin_2021_05_21_05_40_28_Friday.sql.gz
./weekly/sadmin/sadmin_2021_05_28_05_38_10_Friday.sql.gz
./monthly/sadmin
./monthly/sadmin/sadmin_2021_02_01_05_42_18_Monday.sql.gz
./monthly/sadmin/sadmin_2021_03_01_05_40_58_Monday.sql.gz
./monthly/sadmin/sadmin_2021_04_01_05_38_05_Thursday.sql.gz
./monthly/sadmin/sadmin_2021_05_01_05_37_50_Saturday.sql.gz
./yearly/sadmin
./yearly/sadmin/sadmin_2019_12_31_05_56_41_Tuesday.sql.gz
./yearly/sadmin/sadmin_2020_12_31_05_51_04_Thursday.sql.gz
./latest/sadmin_2021_05_29_05_50_39_Saturday.sql.gz
/sadmin/dat/dbb $ 
```

We have 4 'daily' backups (default). The 'latest' directory always contain link to 
the most recent backup. The 'monthly' is taken on the first of each month (Default). We also 
decided to keep 4 copies of the monthly backup. The weekly backup is done every Friday (Default) 
and the 'yearly' backup, will be taken on the 31th of December of each year and the default is to 
keep 2 copies of it.
{: .text-justify}

```bash
# Database Name to exclude from backup, separate each name by the pipe symbol '|'.
#export DBEXCLUDE="information_schema|performance_schema"  
export DBEXCLUDE=""  


# Number of backup to keep per backup type
export DAILY_BACKUP_TO_KEEP=4                                           # Nb. Daily Backup to keep
export WEEKLY_BACKUP_TO_KEEP=4                                          # Nb. Weekly Backup to keep
export MONTHLY_BACKUP_TO_KEEP=4                                         # Nb. Monthly Backup to keep
export YEARLY_BACKUP_TO_KEEP=2                                          # Nb. Yearly Backup to keep

# What day/date per backup type
export WEEKLY_BACKUP_DAY=5                                              # Day Week Backup 1=Mon7=Sun
export MONTHLY_BACKUP_DATE=1                                            # Monthly Backup Date (1-28)
export YEARLY_BACKUP_MONTH=12                                           # Yearly Backup Month (1-12)
export YEARLY_BACKUP_DATE=31                                            # Yearly Backup Date (1-28)
```

If you wish to change the value of any of the variables below, it is recommended to copy the script 
to the user directory (${SADMIN}/usr/bin), so it's not replaced by a future version of this script. 
In future version, we will allow these variables to be specify on the command line or within the
SADMIN configuration file. 
{: .text-justify}

[Back to the top](#top_of_page)



<a id="examples"></a>
## EXAMPLE

```bash
# sadm_backupdb.sh 
================================================================================
Sat May 29 10:12:13 EDT 2021 - sadm_backupdb.sh V2.3 - SADM Lib. V3.70
Server Name: holmes.maison.ca - Type: LINUX
CENTOS 7.9.2009 Kernel 3.10.0-1160.25.1.el7.x86_64
==================================================
 
----------Setup Backup Environment ...
 - Backup All Databases.
 - Compress the backup file.
 - Keep 4 daily backups.
 - Keep 4 weekly backups.
 - Keep 4 monthly backups.
 - Keep 2 yearly backups.
 - Do the weekly backup on Friday.
 - Do the monthly backup on the 1 of every month.
 - Do the yearly backup on the 31 of December every year.

----------
Starting Backup of Database sadmin.
Backup Directory is /sadmin/dat/dbb/daily/sadmin
Backup FileName is sadmin_2021_05_29_10_12_14_Saturday.sql.gz
Running mysqldump ...
[SUCCESS] Backup Succeeded 

----------
Starting Backup of Database wordpress.
Backup Directory is /sadmin/dat/dbb/daily/wordpress
Backup FileName is wordpress_2021_05_29_10_12_14_Saturday.sql.gz
Running mysqldump ...
[SUCCESS] Backup Succeeded 

----------

Cleaning daily Backup (Keep last 4 Backups).
    - Pruning /sadmin/dat/dbb/daily/sadmin Database Backup.
      - 1 Backup(s) out of 5 will be remove.
      - Deleting file sadmin_2021_05_26_13_05_06_Wednesday.sql.gz ...
    - Pruning /sadmin/dat/dbb/daily/wordpress Database Backup.
      - 1 Backup(s) out of 5 will be remove.
      - Deleting file wordpress_2021_05_26_13_05_06_Wednesday.sql.gz ...

Cleaning weekly Backup (Keep last 4 Backups).
    - Pruning /sadmin/dat/dbb/weekly/sadmin Database Backup.
      - No Backup to delete (We have now 4 backup file(s)).
    - Pruning /sadmin/dat/dbb/weekly/wordpress Database Backup.
      - No Backup to delete (We have now 4 backup file(s)).

Cleaning monthly Backup (Keep last 4 Backups).
    - Pruning /sadmin/dat/dbb/monthly/sadmin Database Backup.
      - No Backup to delete (We have now 4 backup file(s)).
    - Pruning /sadmin/dat/dbb/monthly/wordpress Database Backup.
      - No Backup to delete (We have now 4 backup file(s)).

Cleaning yearly Backup (Keep last 2 Backups).
    - Pruning /sadmin/dat/dbb/yearly/sadmin Database Backup.
      - No Backup to delete (We have now 2 backup file(s)).
    - Pruning /sadmin/dat/dbb/yearly/wordpress Database Backup.
      - No Backup to delete (We have now 2 backup file(s)).

==================================================
Script exit code is 0 (Success) and execution time is 00:00:06
History (/sadmin/dat/rch/holmes_sadm_backupdb.rch) trim to 35 lines.
Script will send an alert only when it terminate with error ($SADM_ALERT_TYPE=1).
Script succeeded, no alert will be send to 'default' alert group.
New log (/sadmin/log/holmes_sadm_backupdb.log) created ($SADM_LOG_APPEND='N').
End of sadm_backupdb.sh - Sat May 29 10:12:15 EDT 2021
================================================================================
```

[Back to the top](#top_of_page)


{% include {{ site.section_options     }} %}
| **[ -b backup_dir]** | Specify backup directory | 
| **[ -u ]** | Don't compress the output backup | 
| **[ -n dbname ]** | To only backup specified database | 


{% include {{ site.section_environment }} %}

{% include {{ site.section_exitcode    }} %}

{% include {{ site.section_author      }} %}

{% include {{ site.section_copyright   }} %}


<a id="seealso"></a>
## SEE ALSO

[sadm_server-sunrise.sh]({% post_url 2021-05-26-sadm-server-sunrise %}) - Collect & process data produced by all actives clients  
[sadm_server_housekeeping.sh]({% post_url 2021-05-27-sadm-server-housekeeping %}) - Purge old log,rch,nmon files and check $SADMIN permission   
[sadm_daily_farm_fetch.sh]({% post_url 2021-05-28-sadm-daily-farm-fetch %}) - Collect Hardware/Software/Performance data from actives servers   
[sadm_database_update.py]({% post_url 2021-05-29-sadm-database-update %}) - Take data collected from clients and update database    
[sadm_nmon_rrd_update.sh]({% post_url 2021-05-29-sadm-nmon-rrd-update %}) - Daily performance database update   
[sadm_subnet-lookup.py]({% post_url 2021-05-29-sadm-subnet-lookup %}) - Scan network selected subnet & store info in database  
[sadmin.cfg]({% post_url 2021-04-26-sadmin-cfg %}) - SADMIN main configuration file  
[sadm_backup.sh]({% post_url 2021-05-24-sadm-backup %}) - Backup based on the content of the backup list & exclude file  
