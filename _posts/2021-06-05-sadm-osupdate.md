---
title:          sadm_osupdate.sh
desc:           Perform operating system update of current server
version:        3.26
updated:        2021-06-05
os:             Linux
type:           C  # [D]oc [S]=Server only [C]=Client [B]oth
categories:     [ utilities ] 
#categories:     [ how-to, web_interface, backup, configuration-files, system_monitor, server-scripts, client-scripts, command_line,  utilities, libraries, templates, test ] 
tags:           [ utilities ] 
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



<a id="name"></a>
## NAME
**{{ page.title }}**  
*{{ page.desc }}*   



<a id="synopsis"></a>
## SYNOPSIS

```bash
{{ page.title }} [-d 0-9] [-h] [-r] [-v]
```

{% include sadm/sadm_page_info.md %}
{% if page.type == "S" %}
<font size="3"><strong>Can only be run on SADMIN Server.</strong></font>
{% endif %}
{% if page.type == "B" %}
<font size="3"><strong>Can be executed on a client and on the SADMIN Server.</strong></font>
{% endif %}




<a id="description"></a>
## DESCRIPTION
When you schedule an operating system update this is the script that is responsible of doing it.
It apply all pending Operating System update on the current system, it can be executed only by the 
'root' user (or with sudo). No question will be asked when running this script.
It support Redhat, CentOS, Fedora, Ubuntu, Debian (family) and Raspbian.
To prevent a SADMIN server outage, no automatic reboot will be performed on the SADMIN server.
Remember that every SADMIN script produce a 'log' and an 'rch' file, that you can consult afterward.  
{: .text-justify}

Every schedule for operating system update are contained in a dedicated crontab file 
(/etc/cron.d/sadm_osupdate). This crontab is updated if necessary every 5 minutes by the "[sadm_fetch_client.sh]({% post_url 2021-03-16-sadm-fetch-client %}) script. You will notice that the [sadm_osupdate_starter.sh]({% post_url 2021-06-06-sadm-osupdate-starter %}) script is responsible to run the O/S update on the selected 
remote system.
{: .text-justify}

**Example of the O/S update crontab (/etc/cron.d/sadm_osupdate)**

```bash
# SADMIN - Operating System Update Schedule
# Please don't edit manually, SADMIN generated.
SADMIN=/opt/sadmin
# 
30 05 * * 01 sadmin sudo ${SADMIN}/bin/sadm_osupdate_starter.sh rhel8 >/dev/null 2>&1
33 05 * * 05 sadmin sudo ${SADMIN}/bin/sadm_osupdate_starter.sh ubuntu2004 >/dev/null 2>&1
00 03 * * 04 sadmin sudo ${SADMIN}/bin/sadm_osupdate_starter.sh centos8 >/dev/null 2>&1
30 03 * * 01 sadmin sudo ${SADMIN}/bin/sadm_osupdate_starter.sh debian10 >/dev/null 2>&1
```


<a id="schedule_osupdate"></a>
### Schedule an automated operating system update

If you want you schedule an operating system update using the SADMIN web interface. First, click on
the word "O/S Update" in the heading portion of the web interface.
![OS Update Button](/assets/img/sadm_osupdate/sadm_osupdate_button.png)
{: .align-center}

Then click on the server name you want to create or update the schedule.  
![OS Update Choose Server](/assets/img/sadm_osupdate/sadm_osupdate_choose_server.png)
{: .align-center}

Then the page below will appear, allowing you to modify or deactivate a schedule. 

<dl>
<dt><b>Activate O/S Update Schedule</b></dt>
<dd>If you don't want to schedule an operating system update, make sure the field "Activate O/S Update Schedule" 
is set to "No". This is the default when you create a new server is "No". </dd>
<dd>If you want to schedule an automatic operating system update set this field to "Yes".</dd>
</dl>

<dl>
<dt><b>Reboot after O/S update</b></dt>
<dd>If you don't want a reboot after an operating system update set this field to "No".</dd>
<dd>This is the default value when you add a new system.</dd>
<dd>If you want to reboot after an operating system update set this field to "Yes".</dd>
<dd>    - Even if this field is set to "Yes", no unnecessary reboot will be done if no update were applied.</dd>
<dd>    - To prevent a SADMIN server outage, no automatic reboot will be performed on this server.</dd>
</dl>

![OS Update Schedule](/assets/img/sadm_osupdate/sadm_osupdate_schedule.png)
{: .align-center}

<dl>
<dt><b>Month(s) to run the O/S Update</b></dt>
<dd>This selection list, let you to choose what are the month(s) you allow an operating system update
to happen. If you would want to perform update only in "June", select the month of June. </dd>
<dd>The default is to allow operating system update to perform in any month of the year (No 
restriction based on the month).</dd>
</dl>

<dl>
<dt><b>Date to perform the update</b></dt>
<dd>This selection list, allow you to choose to update your system on particular date(s). Let say
you want to update your system on the 15th of the month, select "15th of the month". </dd>
<dd>The default is "Any date of the month" to allow operating system update to perform on any date 
of the month. (No restriction based on date).</dd>
</dl>

<dl>
<dt><b>Day of the update O/S</b></dt>
<dd>This selection list, allow you to choose the day of the week you would like to update your 
system. </dd>
<dd>The default is "All Run any day of the week", this means an update would run every day of the
week. (No restriction based on day).</dd>
</dl>


<dl>
<dt><b>Time to Update the O/S</b></dt>
<dd>This field allow you to specify the time of the operating system will be updated.</dd>
<dd>The default is set to "01:00 am".</dd>
</dl>


#### Result of the update can by seen on the O/S Update Schedule Status page
- You can click on the server name to modify the schedule.
- If you want to view the log of the last update, click on "[log]".
- If you want to view the execution history of the o/s update on "[rch]".
- You can see the date of the last and the next update.
- You can view at what occurrence the o/s update is executed.

![OS Update Schedule](/assets/img/sadm_osupdate/sadm_osupdate_status.png)
{: .align-center}



**Example of screen output when running the script on a Ubuntu system**  

```bash
root@ubuntu2004:~  # sadm_osupdate.sh
================================================================================
Sun 06 Jun 2021 07:33:09 PM EDT - sadm_osupdate.sh V3.26 - SADM Lib. V3.70
Server Name: ubuntu2004.maison.ca - Type: LINUX
UBUNTU 20.04 Kernel 5.8.0-55-generic
==================================================

Verifying update availability for UBUNTU v20.04
Start with a clean of APT cache, running 'apt-get clean'
[ OK ] APT cache is now cleaned.

Update the APT package repository cache with 'apt-get update'
[ OK ] The cache have been updated.


Retrieving list of upgradable packages.
Running 'apt list --upgradable'.
[ OK ] No Update available.


==================================================
Script exit code is 0 (Success) and execution time is 00:00:22
History (/opt/sadmin/dat/rch/ubuntu2004_sadm_osupdate.rch) trim to 35 lines. 
Script will send an alert only when it terminate with error ($SADM_ALERT_TYPE=1).
Script succeeded, no alert will be send to 'default' alert group.
New log (/opt/sadmin/log/ubuntu2004_sadm_osupdate.log) created ($SADM_LOG_APPEND='N').
End of sadm_osupdate.sh - Sun 06 Jun 2021 07:33:23 PM EDT
================================================================================
```

[Back to the top](#top_of_page)



<a id="examples"></a>
## EXAMPLE
**Example of screen output when running the script on a Red Hat 8 system**  

```bash
[root@rhel8 ~]# sadm_osupdate.sh
================================================================================
Sun Jun  6 19:43:04 EDT 2021 - sadm_osupdate.sh V3.26 - SADM Lib. V3.70
Server Name: rhel8.maison.ca - Type: LINUX
REDHAT 8.4 Kernel 4.18.0-305.el8.x86_64
==================================================

Verifying update availability for REDHAT v8.4
Checking if update are available, with 'dnf check-update'.
[ OK ] No Update available.

==================================================
Script exit code is 0 (Success) and execution time is 00:00:17
History (/opt/sadmin/dat/rch/rhel8_sadm_osupdate.rch) trim to 35 lines.
Script will send an alert only when it terminate with error ($SADM_ALERT_TYPE=1).
Script succeeded, no alert will be send to 'default' alert group.
New log (/opt/sadmin/log/rhel8_sadm_osupdate.log) created ($SADM_LOG_APPEND='N').
End of sadm_osupdate.sh - Sun Jun  6 19:43:13 EDT 2021
================================================================================

```
<!-- ![Daily Script Report Example](/assets/img/man/sadm_daily_report_script.png){: .align-center} -->

[Back to the top](#top_of_page)


{% include {{ site.section_options     }} %}
| **-r** | Reboot server after update, if update applied |
| | & if 'Reboot after O/S Update' field is set to "Yes" | 

{% include {{ site.section_environment }} %}

{% include {{ site.section_exitcode    }} %}

{% include {{ site.section_author      }} %}

{% include {{ site.section_copyright   }} %}


<a id="seealso"></a>
## SEE ALSO

[How-to Add a client]({% post_url 2021-04-11-web-add-client %}) - How-to add a client to SADMIN inventory  
[How-to Remove a client]({% post_url 2021-05-19-how-to-remove-a-client %}) - How-to remove a client from SADMIN inventory  
[sadmin.cfg]({% post_url 2021-04-26-sadmin-cfg %}) - SADMIN main configuration file   
[sadm_osupdate.sh]({% post_url 2021-06-05-sadm-osupdate %}) - Perform Operating System update on the current server  
[sadm_osupdate_starter.sh]({% post_url 2021-06-06-sadm-osupdate-starter %}) - Run the O/S update to selected remote system   
