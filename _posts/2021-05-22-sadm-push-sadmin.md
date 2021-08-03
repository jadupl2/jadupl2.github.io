---
title:          sadm_push_sadmin.sh
permalink:      /sadm-push-sadmin/
desc:           Push SADMIN version to one or all actives clients.
version:        2.2
updated:        2021-05-22
os:             Linux, Aix, MacOS
tags:           [ server-scripts ] 
categories:     [ utilities ] 
# [D]oc [S]=Server only [C]=Client [B]oth
type:           S  
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
{{ page.title }} [-d 0-9] [-h] [-n hostname ] [-s] [-u] [-v]
```
{% if page.type == "S" %}
<font size="3"><strong>Can only be run on SADMIN Server.</strong></font>
{% endif %}
{% if page.type == "B" %}
<font size="3"><strong>Can be executed on a client and on the SADMIN Server.</strong></font>
{% endif %}




<a id="description"></a>
## DESCRIPTION

This script copy the SADMIN version of the master to one or all actives clients. If you want to 
update only one client, use the command line option '-n' and specify the hostname to update.
Let's say you have just updated your SADMIN master server and you want to update all your clients, 
this is the script to run. By default, this script is not part of any crontab job, so you need 
to execute it manually or place it in the server crontab (/etc/cron.d/sadm_server). Non-active 
clients (status set to inactive in CRUD) are ignored. Directories others than the one 
specified below are left untouched on the client. So don't worry, it will update only SADMIN files 
and scripts, your SADMIN configuration files, scripts (in $SADMIN/usr/bin) are left untouched by 
this push.   
{: .text-justify}
- Use the '-s' to push the startup & shutdown script to all your clients. This option is useful 
if you are using the same startup and shutdown scripts for all your clients.
- The '-u' option allow you to also push the "$SADMIN/usr" directories to the clients.


**Operations done for each active clients :**

- Verify if SSH connection to client is working.  
- Get the directory where SADMIN is install on client via '/etc/environment'.  
- Copy scripts directory ($SADMIN/bin) to corresponding client directory.  
- Copy packages directory ($SADMIN/pkg) to client directory.  
- Copy libraries directory ($SADMIN/lib) to client directory. 
- Copy the alert group and Slack configuration files to client directory. 
- If user directory option is used ('-u').  
    - Copy user directories ($SADMIN/usr/bin,$SADMIN/usr/lib,$SADMIN/usr/cfg) to client.  
- Copy dot configuration template files from ($SADMIN/cfg) to client directory.  
- Copy dot configuration template files from ($SADMIN/sys) to client directory.  
- If system startup/shutdown directory option is used ('-s').    
    - Copy customized scripts of Startup/Shutdown ($SADMIN/sys) to client. 
    - See how to use the startup/shutdown script with [sadm_service.sh]({% post_url 2021-05-23-sadm-service-ctrl %})
- System Monitor scripts and templates
  - Copy 'nmon' watcher scripts ($SADMIN/usr/mon/swatch_nmon.sh) to client.  
  - Copy 'nmon' error text file ($SADMIN/usr/mon/swatch_nmon.txt) to client.          
  - Copy Monitor template script ($SADMIN/usr/mon/stemplate.sh) to client. 
  - Copy Monitor Service Restart script ($SADMIN/usr/mon/srestart.sh) to client.  


[Back to the top](#top_of_page)



<a id="examples"></a>
## EXAMPLE
 
```bash
root@holmes:~ # sadm_push_sadmin.sh 
================================================================================
Sat May 22 11:37:05 EDT 2021 - sadm_push_sadmin.sh V2.30 - SADM Lib. V3.70
Server Name: holmes.maison.ca - Type: LINUX
CENTOS 7.9.2009 Kernel 3.10.0-1160.25.1.el7.x86_64
==================================================
 
----------
Processing (1) borg.maison.ca 
[ OK ] SSH to borg.maison.ca
[ OK ] SADMIN is install in /opt/sadmin.
[ OK ] rsync -ar --delete /sadmin/bin/ borg.maison.ca:/opt/sadmin/bin/
[ OK ] rsync -ar --delete /sadmin/pkg/ borg.maison.ca:/opt/sadmin/pkg/
[ OK ] rsync -ar --delete /sadmin/lib/ borg.maison.ca:/opt/sadmin/lib/
[ OK ] rsync -a /sadmin/cfg/alert_group.cfg borg.maison.ca:/opt/sadmin/cfg/alert_group.cfg
[ OK ] rsync -a /sadmin/cfg/alert_slack.cfg borg.maison.ca:/opt/sadmin/cfg/alert_slack.cfg
[ OK ] rsync -ar --delete /sadmin/cfg/.??* borg.maison.ca:/opt/sadmin/cfg/
[ OK ] rsync -ar --delete /sadmin/sys/.??* borg.maison.ca:/opt/sadmin/sys/
[ OK ] rsync -ar --delete /sadmin/usr/mon/swatch_nmon.sh borg.maison.ca:/opt/sadmin/usr/mon/swatch_nmon.sh
[ OK ] rsync -ar --delete /sadmin/usr/mon/swatch_nmon.txt borg.maison.ca:/opt/sadmin/usr/mon/swatch_nmon.txt
[ OK ] rsync -ar --delete /sadmin/usr/mon/stemplate.sh borg.maison.ca:/opt/sadmin/usr/mon/stemplate.sh
[ OK ] rsync -ar --delete /sadmin/usr/mon/srestart.sh borg.maison.ca:/opt/sadmin/usr/mon/srestart.sh

----------
Processing (2) centos6.maison.ca 
[ WARNING ] Can't SSH to sporadic server centos6.maison.ca
...
...
```

**Example using command line option :**  
-u   Also sync $SADMIN/usr/bin, $SADMIN/usr/lib and $SADMIN/usr/cfg to all active clients    
-n   Push SADMIN version only to system specified  
-s   Also sync $SADMIN/sys to all active clients  

![sadm_pusg_sadmin_us.png](/assets/img/sadm_push_sadmin_us.png){: .align-center}

[Back to the top](#top_of_page)




{% include {{ site.section_options     }} %}
| **-n hostname** | Push SADMIN version only to system specified | 
| **-s** | Also sync $SADMIN/sys to all active clients | 
| **-u** | Also sync $SADMIN/usr/bin to all active clients | 


{% include {{ site.section_environment }} %}

{% include {{ site.section_exitcode    }} %}

{% include {{ site.section_author      }} %}

{% include {{ site.section_copyright   }} %}


<a id="seealso"></a>
## SEE ALSO

[sadm_service_ctrl.sh]({% post_url 2021-05-23-sadm-service-ctrl %}) - Enable, Disable and get status of system startup and shutdown script  
[SADMIN installation](/_pages/install) - SADMIN installation page    
[How-to Add a client]({% post_url 2021-04-11-web-add-client %}) - How-to add a client to SADMIN inventory  
[How-to Remove a client]({% post_url 2021-05-19-how-to-remove-a-client %}) - How-to remove a client from SADMIN inventory  
[How-to update SADMIN]({% post_url 2021-03-14-sadm-update %}) - How-to update to latest version of SADMIN   

