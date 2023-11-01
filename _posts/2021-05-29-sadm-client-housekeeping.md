---
title:          sadm_client_housekeeping.sh
permalink:      /sadm-client-housekeeping/
desc:           Set $SADMIN owner/group/permission, prune old log & rch files,check sadmin account.
version:        2.06
updated:        2022-07-28
os:             Linux, Aix, MacOS
type:           C  # [D]oc [S]=Server only [C]=Client [B]oth
tags:           [ client-scripts ] 
categories:     [ client-scripts ] 
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
{{ page.title }} [-d 0-9] [-h] [-v]
```
{% if page.type == "S" %}
<font size="3"><strong>Can only be run on SADMIN Server.</strong></font>
{% endif %}
{% if page.type == "B" %}
<font size="3"><strong>Can be executed on a client and on the SADMIN Server.</strong></font>
{% endif %}




<a id="description"></a>
## DESCRIPTION
The function of this script is to perform various housekeeping, such as deleting old logs and 
history files not used for a number of days specified in the SADMIN configuration file. It also 
make sure that the permission within the $SADMIN are in good condition to allow proper utilization 
of the SADMIN tools.
{: .text-justify}

**Here is a list of the various functions executed by this script**

- Make sure all the server files in "$SADMIN" have proper owner, group and permission  
- Remove files older than 7 days in "$SADMIN/tmp" directory  
- Remove pid files (once a day) in “$SADMIN/tmp” that prevent script from not running    
- Remove \*.rch files in "${SADMIN}/dat/rch" older than "[${SADM_RCH_KEEPDAYS}]({% post_url 2021-04-26-sadmin-cfg %}/#sadm_rch_keepdays)"
- Remove \*.log files in "${SADMIN}/log" older than "[${SADM_LOG_KEEPDAYS}]({% post_url 2021-04-26-sadmin-cfg %}/#sadm_log_keepdays)"
- Remove \*.nmon files in "${SADMIN}/dat/nmon" older than "[${SADM_NMON_KEEPDAYS}]({% post_url 2021-04-26-sadmin-cfg %}/#sadm_nmon_keepdays)"
- Check existence on the server of "[$SADMIN_USER" and "$SADMIN_GROUP]({% post_url 2021-04-26-sadmin-cfg %}/#sadm_user)"
- Verify if "$SADMIN_USER" is not lock or the password is expired  


{: .text-justify}

[Back to the top](#top_of_page)



<a id="examples"></a>
## EXAMPLE

```bash
root@holmes:~ # sadm_client_housekeeping.sh 
================================================================================
Thu 28 Jul 2022 13:00:24 - sadm_client_housekeeping.sh v2.06 - Library v4.03
Desc: Set $SADMIN owner/group/permission, prune old log,rch files ,check sadmin account.
Host: sherlock.maison.ca - User: root - Arch: x86_64 - SADMIN: /opt/sadmin
Almalinux Linux release 9.0 - Kernel 5.14.0-70.17.1.el9_0.x86_64
==================================================
 
SADMIN Client Directories Housekeeping.
  - chmod 0775 /opt/sadmin [ OK ]
  - chown sadmin:sadmin /opt/sadmin [ OK ]
  - chmod 0775 /opt/sadmin/bin [ OK ]
  - chown sadmin:sadmin /opt/sadmin/bin [ OK ]
  - chmod 0775 /opt/sadmin/cfg [ OK ]
  - chown sadmin:sadmin /opt/sadmin/cfg [ OK ]
  - chmod 0775 /opt/sadmin/dat [ OK ]
  - chown sadmin:sadmin /opt/sadmin/dat [ OK ]
  - chmod 0775 /opt/sadmin/doc [ OK ]
  - chown sadmin:sadmin /opt/sadmin/doc [ OK ]
  - chmod 0775 /opt/sadmin/lib [ OK ]
  - chown sadmin:sadmin /opt/sadmin/lib [ OK ]
  - chmod 0775 /opt/sadmin/log [ OK ]
  - chown sadmin:sadmin /opt/sadmin/log [ OK ]
  - chmod 775 /opt/sadmin/pkg [ OK ]
  - chown sadmin:sadmin /opt/sadmin/pkg [ OK ]
  - chmod 775 /opt/sadmin/setup [ OK ]
  - chown sadmin:sadmin /opt/sadmin/setup [ OK ]
  - chmod 0775 /opt/sadmin/sys [ OK ]
  - chown sadmin:sadmin /opt/sadmin/sys [ OK ]
  - chmod 1777 /opt/sadmin/tmp [ OK ]
  - chown sadmin:sadmin /opt/sadmin/tmp [ OK ]
  - chmod 0775 /opt/sadmin/usr [ OK ]
  - chown sadmin:sadmin /opt/sadmin/usr [ OK ]
  - chmod 0775 /opt/sadmin/usr/bin [ OK ]
  - chown sadmin:sadmin /opt/sadmin/usr/bin [ OK ]
  - chmod 0775 /opt/sadmin/usr/lib [ OK ]
  - chown sadmin:sadmin /opt/sadmin/usr/lib [ OK ]
  - chmod 0775 /opt/sadmin/usr/doc [ OK ]
  - chown sadmin:sadmin /opt/sadmin/usr/doc [ OK ]
  - chmod 0775 /opt/sadmin/usr/mon [ OK ]
  - chown sadmin:sadmin /opt/sadmin/usr/mon [ OK ]
  - chmod 0775 /opt/sadmin/dat/nmon [ OK ]
  - chown sadmin:sadmin /opt/sadmin/dat/nmon [ OK ]
  - chmod 0775 /opt/sadmin/dat/dr [ OK ]
  - chown sadmin:sadmin /opt/sadmin/dat/dr [ OK ]
  - chmod 0775 /opt/sadmin/dat/rch [ OK ]
  - chown sadmin:sadmin /opt/sadmin/dat/rch [ OK ]
  - chmod 0775 /opt/sadmin/dat/dbb [ OK ]
  - chown sadmin:sadmin /opt/sadmin/dat/dbb [ OK ]
  - chmod 0775 /opt/sadmin/dat/net [ OK ]
  - chown sadmin:sadmin /opt/sadmin/dat/net [ OK ]

SADMIN Client Files Housekeeping.
  - chmod 0644 /etc/cron.d/sadm_client [ OK ]
  - chown root:root /etc/cron.d/sadm_client [ OK ]
  - chmod 0644 /etc/cron.d/sadm_server [ OK ]
  - chown root:root /etc/cron.d/sadm_server [ OK ]
  - chmod 0644 /etc/cron.d/sadm_osupdate [ OK ]
  - chown root:root /etc/cron.d/sadm_osupdate [ OK ]
  - chmod 0644 /etc/cron.d/sadm_backup [ OK ]
  - chown root:root /etc/cron.d/sadm_backup [ OK ]
  - chmod 0644 /etc/cron.d/sadm_rear_backup [ OK ]
  - chown root:root /etc/cron.d/sadm_rear_backup [ OK ]
  - chmod 0664 /opt/sadmin/readme.md [ OK ]
  - chown sadmin:sadmin /opt/sadmin/readme.md [ OK ]
  - chmod 0664 /opt/sadmin/license [ OK ]
  - chown sadmin:sadmin /opt/sadmin/license [ OK ]
  - chmod 0664 /opt/sadmin/changelog.md [ OK ]
  - chown sadmin:sadmin /opt/sadmin/changelog.md [ OK ]
  - chmod 0640 /opt/sadmin/cfg/.dbpass [ OK ]
  - chown sadmin:sadmin /opt/sadmin/cfg/.dbpass [ OK ]
  - chmod 0640 /opt/sadmin/cfg/.gmpw [ OK ]
  - chown sadmin:sadmin /opt/sadmin/cfg/.gmpw [ OK ]
  - chmod 0600 /etc/postfix/sasl_passwd [ OK ]
  - chown root:root /etc/postfix/sasl_passwd [ OK ]
  - chmod 0600 /etc/postfix/sasl_passwd.db [ OK ]
  - chown root:root /etc/postfix/sasl_passwd.db [ OK ]
  - find /opt/sadmin/tmp -type f -exec chown sadmin:sadmin {} \; [ OK ]
  - find /opt/sadmin/tmp -type f -exec chmod 1777{} \; [ OK ]
  - find /opt/sadmin/dat -type f -exec chown sadmin:sadmin {} \; [ OK ]
  - find /opt/sadmin/dat -type f -exec chmod 0664{} \; [ OK ]
  - find /opt/sadmin/log -type f -exec chown sadmin:sadmin {} \; [ OK ]
  - find /opt/sadmin/log -type f -exec chmod 0666{} \; [ OK ]
  - find /opt/sadmin/usr -type f -exec chown sadmin:sadmin {} \; [ OK ]
  - find /opt/sadmin/usr -type f -exec chmod 0644{} \; [ OK ]
  - find /opt/sadmin/usr/bin -type f -exec chown sadmin:sadmin {} \; [ OK ]
  - find /opt/sadmin/usr/bin -type f -exec chmod 0775{} \; [ OK ]
  - find /opt/sadmin/usr/lib -type f -exec chown sadmin:sadmin {} \; [ OK ]
  - find /opt/sadmin/usr/lib -type f -exec chmod 0775{} \; [ OK ]
  - find /opt/sadmin/usr/mon -type f -exec chown sadmin:sadmin {} \; [ OK ]
  - find /opt/sadmin/usr/mon -type f -exec chmod 0775{} \; [ OK ]
  - find /opt/sadmin/cfg -type f -exec chown sadmin:sadmin {} \; [ OK ]
  - find /opt/sadmin/cfg -type f -exec chmod 0664{} \; [ OK ]
  - find /opt/sadmin/sys -type f -exec chown sadmin:sadmin {} \; [ OK ]
  - find /opt/sadmin/sys -type f -exec chmod 0770{} \; [ OK ]
  - find /opt/sadmin/bin -type f -exec chown sadmin:sadmin {} \; [ OK ]
  - find /opt/sadmin/bin -type f -exec chmod 0775{} \; [ OK ]
  - find /opt/sadmin/lib -type f -exec chown sadmin:sadmin {} \; [ OK ]
  - find /opt/sadmin/lib -type f -exec chmod 0775{} \; [ OK ]
  - find /opt/sadmin/pkg -type f -exec chown sadmin:sadmin {} \; [ OK ]
  - find /opt/sadmin/pkg -type f -exec chmod 0755{} \; [ OK ]

SADMIN Files Pruning.
  - Remove unmodified file(s) for more than 7 days in /opt/sadmin/tmp.
    - find /opt/sadmin/tmp  -type f -mtime +7 -exec rm -f {} \; [ OK ]
  - Remove all pid files once a day - This prevent script from not running.
    - find /opt/sadmin/tmp  -type f -name '*.pid' -exec rm -f {} \; [ OK ]
  - Remove any unmodified *.rch file(s) for more than 40 days in /opt/sadmin/dat/rch.
    - find /opt/sadmin/dat/rch -type f -mtime +40 -name '*.rch' -exec rm -f {} \; [ OK ]
  - Remove any unmodified *.log file(s) for more than 40 days in /opt/sadmin/log.
    - find /opt/sadmin/log -type f -mtime +40 -name '*.log' -exec rm -f {} \; [ OK ]
  - Remove any unmodified *.nmon file(s) for more than 40 days in /opt/sadmin/dat/nmon.
    - find /opt/sadmin/dat/nmon -mtime +40 -type f -name '*.nmon' -exec rm {} \; [ OK ]

Check status of account 'sadmin' ...
  - Making sure account 'sadmin' doesn't expire.
  - Making sure password for 'sadmin' doesn't expire.
  - We recommend changing 'sadmin' password at regular interval.
  - No problem with 'sadmin' account. [ OK ]

Check SADMIN client 'sadmin' crontab & System monitor config file ...
  - Make sure sadm_client crontab (/etc/cron.d/sadm_client) have 'sadm_nmon_watcher.sh' line.
  - Yes, crontab (/etc/cron.d/sadm_client) already got 'sadm_nmon_watcher.sh' line.
  - Making sure that script:swatch_nmon.sh is no longer in /opt/sadmin/cfg/sherlock.smon

==================================================
Script exit code is 0 (Success) and execution time is 00:00:07
History file '$SADMIN/dat/rch/sherlock_sadm_client_housekeeping.rch' trim to 35 lines.
Script is set to send an alert only when it terminate with error.
Script succeeded, no alert will be send ($SADM_ALERT_TYPE=1).
New log created '$SADMIN/log/sherlock_sadm_client_housekeeping.log'.
End of sadm_client_housekeeping.sh - Thu 28 Jul 2022 01:00:25 PM EDT
================================================================================
```
<!-- ![Daily Script Report Example](/assets/img/man/sadm_daily_report_script.png){: .align-center} -->

[Back to the top](#top_of_page)


{% include {{ site.section_options     }} %}

{% include {{ site.section_environment }} %}

{% include {{ site.section_exitcode    }} %}

{% include {{ site.section_author      }} %}

{% include {{ site.section_copyright   }} %}


<a id="seealso"></a>
## SEE ALSO

[sadm_create_sysinfo.sh]({% post_url 2021-04-22-sadm-create-sysinfo %}) - Collect hardware & software information about the system   
[System Information File]({% post_url 2021-05-30-sysinfo-file %}) - Documentation about the system information file  
[sadm_client_sunset.sh]({% post_url 2021-05-31-sadm-client-sunset %}) - Clients end of day housekeeping and producing system information files  
[sadm_fetch_clients.sh]({% post_url 2021-03-16-sadm-fetch-clients %}) - rsync all .rch/.log/.rpt from actives clients to the SADMIN server. 