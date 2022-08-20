---
title:          sadm_create_sysinfo.sh
permalink:      /sadm-create-sysinfo/
desc:           Collect hardware & software information about the system
version:        3.33
updated:        2022-07-28
os:             Linux, Aix, MacOS
type:           B  # [D]oc [S]=Server only [C]=Client [B]oth
tags:           [ client-scripts, web_interface ] 
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
<font size="3">Can only be run on SADMIN Server.</font>
{% endif %}



<a id="description"></a>
## DESCRIPTION

This script is use to collect different software and hardware about the system you are running it 
and record this information in the [System Information File]({% post_url 2021-05-30-sysinfo-file %}). 
When you run this script, no question is asked and information 
collected are stores in the disaster recovery directory ($SADMIN/dat/dr). This script is part of 
the 'client sunset script' (${SADMIN}/bin/sadm_client_sunset.sh). The 'client sunset script' is 
scheduled to run daily from the client crontab (/etc/cron.d/sadm_client). You can also run it 
manually whenever you want to update files in the disaster recovery information directory.
{: .text-justify}


<a id="examples"></a>
## EXAMPLE

```bash
root@holmes:~ # sadm_create_sysinfo.sh 
================================================================================
Thu 28 Jul 2022 13:06:42 - sadm_create_sysinfo.sh v3.33 - Library v4.03
Desc: Collect hardware & software info of system
Host: sherlock.maison.ca - User: root - Arch: x86_64 - SADMIN: /opt/sadmin
Almalinux Linux release 9.0 - Kernel 5.14.0-70.17.1.el9_0.x86_64
==================================================
 
Verifying command availability ...
Creating /opt/sadmin/dat/dr/sherlock_diskinfo.txt ...
Creating /opt/sadmin/dat/dr/sherlock_lvm.txt ...
Creating /opt/sadmin/dat/dr/sherlock_network.txt ...
Creating /opt/sadmin/dat/dr/sherlock_system.txt ...
Creating /opt/sadmin/dat/dr/sherlock_lshw.html ...
Creating /opt/sadmin/dat/dr/sherlock_sysinfo.txt ...
Getting last O/S Update date from /opt/sadmin/dat/rch/sherlock_sadm_osupdate.rch ...
2022.07.24 02:22:14 - Success ...

==================================================
Script exit code is 0 (Success) and execution time is 00:00:15
History file '$SADMIN/dat/rch/sherlock_sadm_create_sysinfo.rch' trim to 35 lines.
Script is set to send an alert only when it terminate with error.
Script succeeded, no alert will be send ($SADM_ALERT_TYPE=1).
New log created '$SADMIN/log/sherlock_sadm_create_sysinfo.log'.
End of sadm_create_sysinfo.sh - Thu 28 Jul 2022 01:06:52 PM EDT
================================================================================
```


Information in the Disaster Recovery directory, will be useful in case of complete system rebuild. 
Files in this directory ($SADMIN/dat/dr) are updated daily.

![sadm_create_sysinfo_files.png](/assets/img/sadm_create_sysinfo_files.png){: .align-center}

To view information generated from this script from the web interface, choose "Systems" options 
from the heading line.
![sadm_create_sysinfo_system.png](/assets/img/sadm_create_sysinfo_system.png){: .align-center}

Then choose the server you want to view the information by clicking on it's name.
![sadm_create_sysinfo_choose_system.png](/assets/img/sadm_create_sysinfo_choose_system.png){: .align-center}

The server main information screen will be shown like below.
![sadm_create_sysinfo_web_buttons.png](/assets/img/sadm_create_sysinfo_web_buttons.png){: .align-center}

This is an example of what you would get by pressing the 'Server Summary' button.
![sadm_create_sysinfo_web_info.png](/assets/img/sadm_create_sysinfo_web_info.png){: .align-center}



 

{% include {{ site.section_options     }} %}

{% include {{ site.section_environment }} %}

{% include {{ site.section_exitcode    }} %}

{% include {{ site.section_author      }} %}

{% include {{ site.section_copyright   }} %}


<a id="seealso"></a>
## SEE ALSO

[sadm_fetch_clients.sh]({% post_url 2021-03-16-sadm-fetch-clients %}) - rsync all .rch/.log/.rpt from actives clients to the SADMIN Server.     
[sadm_requirements.sh]({% post_url 2019-03-21-sadm-requirements %}) - List/Install required SADMIN Tools packages  
[sadm_template.sh]({% post_url 2021-03-16-sadm-template-sh %}) - Using SADMIN Shell script template   
[sadm_template.py]({% post_url 2021-03-16-sadm-template-py %}) - Using SADMIN Python script template    
[sadm_template_menu.sh]({% post_url 2021-04-30-sadm-template-menu %}) - Using SADMIN shell menu template   
[sadm_wrapper.sh]({% post_url 2018-02-11-sadm-wrapper %}) - Use to run your existing scripts & benefit of SADMIN tools  
[sadmlib_std_demo.sh]({% post_url 2019-10-12-sadmlib-std-demo-sh %}) - SADMIN Shell Library Functions Demo   
[sadmlib_std_demo.py]({% post_url 2019-10-12-sadmlib-std-demo-py %}) - SADMIN Python Library Functions Demo  
[SADMIN installation](/_pages/install) - SADMIN installation page.    
