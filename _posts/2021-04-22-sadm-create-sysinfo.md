---
title:          sadm_create_sysinfo.sh
desc:           Collect hardware & software information about the system
version:        3.21 
updated:        2021-06-03
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
Sat May 22 10:51:25 EDT 2021 - sadm_create_sysinfo.sh V3.23 - SADM Lib. V3.70
Server Name: holmes.maison.ca - Type: LINUX
CENTOS 7.9.2009 Kernel 3.10.0-1160.25.1.el7.x86_64
==================================================
 
Verifying command availability ...
Creating /sadmin/dat/dr/holmes_diskinfo.txt ...
Creating /sadmin/dat/dr/holmes_lvm.txt ...
Creating /sadmin/dat/dr/holmes_network.txt ...
Creating /sadmin/dat/dr/holmes_system.txt ...
Creating /sadmin/dat/dr/holmes_lshw.html ...
Creating /sadmin/dat/dr/holmes_sysinfo.txt ...
Getting last O/S Update date from /sadmin/dat/rch/holmes_sadm_osupdate.rch ...

==================================================
Script exit code is 0 (Success) and execution time is 00:00:24
History ($SADMIN/dat/rch/holmes_sadm_create_sysinfo.rch) trim to 35 lines.
Script will send an alert only when it terminate with error ($SADM_ALERT_TYPE=1).
Script succeeded, no alert will be send to 'default' alert group.
New log (/sadmin/log/holmes_sadm_create_sysinfo.log) created ($SADM_LOG_APPEND='N').
End of sadm_create_sysinfo.sh - Sat May 22 10:51:45 EDT 2021
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
