---
title:          sadm_osupdate_starter.sh
desc:           Run the O/S update to selected remote system
version:        4.5
updated:        2021-06-06
os:             Linux
type:           S  # [D]oc [S]=Server only [C]=Client [B]oth
categories:     [ utilities ] 
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
{{ page.title }} [-d 0-9] [-h] [-v] [hostname]
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
The function of this script is to start the O/S update on the remote system it receive as a parameter.
The script read the system information from the database and if a reboot is allowed after the
update of the system, the option "-r" is passed to the [sadm_osupdate.sh]({% post_url 2021-06-05-sadm-osupdate %})
script.
{: .text-justify}

Since we know that the update will be running on the remote system, we don't want to be alerted 
that the system doesn't respond (may be the system is rebooting after the update), a lock file
($SADMIN/tmp/hostname.lock) is created before launching the update on the remote system. When 
the O/S update is finished this lock file is removed. All SADMIN scripts check this lock file
before issuing an alert, if it exist then no alert is issued.
{: .text-justify}
 
[Back to the top](#top_of_page)



<a id="examples"></a>
## EXAMPLE

```bash
# sadm_osupdate_starter.sh fedora33
================================================================================
Mon Jun  7 12:44:52 EDT 2021 - sadm_osupdate_starter.sh V4.5 - SADM Lib. V3.70
Server Name: holmes.maison.ca - Type: LINUX
CENTOS 7.9.2009 Kernel 3.10.0-1160.25.1.el7.x86_64
==================================================
 
[ OK ] Ping host fedora33.maison.ca.
[ OK ] '/opt/sadmin/bin/sadm_osupdate.sh' exist & executable on fedora33.maison.ca.
[ OK ] Lock File (/sadmin/tmp/fedora33.lock) created, monitoring suspended.
 
Starting the O/S update on 'fedora33'.
/bin/ssh -qnp32 fedora33.maison.ca '/opt/sadmin/bin/sadm_osupdate.sh -r'

================================================================================
Mon 07 Jun 2021 12:45:11 PM EDT - sadm_osupdate.sh V3.26 - SADM Lib. V3.70
Server Name: fedora33.maison.ca - Type: LINUX
FEDORA 33 Kernel 5.12.8-200.fc33.x86_64
==================================================
 
Verifying update availability for FEDORA v33
Checking for new update, with 'dnf check-update'
[ OK ] Update available.
----------
Starting FEDORA update process ...
Running : dnf -y update
Return Code after dnf program update is 0.
----------

==================================================
Script exit code is 0 (Success) and execution time is 00:01:09
History (/opt/sadmin/dat/rch/fedora33_sadm_osupdate.rch) trim to 35 lines.
Script will send an alert only when it terminate with error ($SADM_ALERT_TYPE=1).
Script succeeded, no alert will be send to 'default' alert group.
New log (/opt/sadmin/log/fedora33_sadm_osupdate.log) created ($SADM_LOG_APPEND='N').
End of sadm_osupdate.sh - Mon 07 Jun 2021 12:46:03 PM EDT
================================================================================


O/S Update completed on 'fedora33'.
[ OK ] Lock File (/sadmin/tmp/fedora33.lock) removed.

==================================================
Script exit code is 0 (Success) and execution time is 00:01:16
History (/sadmin/dat/rch/holmes_sadm_osupdate_starter.rch) trim to 60 lines.
Script will send an alert only when it terminate with error ($SADM_ALERT_TYPE=1).
Script succeeded, no alert will be send to 'default' alert group.
Log /sadmin/log/holmes_sadm_osupdate_starter.log trim to 5000 lines ($SADM_MAX_LOGLINE=5000).
End of sadm_osupdate_starter.sh - Mon Jun  7 12:46:04 EDT 2021
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

[sadm_fetch_client.sh]({% post_url 2021-03-16-sadm-fetch-client %}) - rsync all .rch/.log/.rpt from actives clients to the SADMIN server.  
[sadm_osupdate.sh]({% post_url 2021-06-05-sadm-osupdate %}) - Perform Operating System update on the current server  
[sadm_osupdate_starter.sh]({% post_url 2021-06-06-sadm-osupdate-starter %}) - Run the O/S update to selected remote system   
