---
title:          sadm_uninstall.sh
permalink:      /sadm-uninstall/
desc:           Uninstall the SADMIN tools.
version:        1.9
updated:        2021-05-21
os:             Linux, Aix, MacOS
type:           B  # [D]oc [S]=Server only [C]=Client [B]oth
tags:           [ utilities ] 
categories:     [ utilities ] 
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
{{ page.title }} [-d 0-9] [-h] [-v] [-y]
```
{% if page.type == "S" %}
<font size="3">Can only be run on SADMIN Server.</font>
{% endif %}



<a id="description"></a>
## DESCRIPTION

This script is use to uninstall a SADMIN Client or Server tools from one system. The script 
detect if it is running on a client or SADMIN server (looking at $SADMIN/cfg/sadmin.cfg). For 
security reason, when you run the script it will run in 'dry run' mode. This means 
that it will not change or remove anything on the system. But it will show you what it would do 
when you really uninstall SADMIN. To really uninstall the SADMIN tools, use the '-y' command line 
option. Be aware that the SADMIN database will be deleted (drop) when uninstalling a SADMIN server 
installation, this is why the database password is asked during a server uninstall. The database 
users 'sadmin' and 'squery' will also be deleted. Lastly, the uninstall will not remove any O/S 
packages, that were installed (if any) during installation, because you may use one of these 
packages for some others purposes.
{: .text-justify}

[Back to the top](#top_of_page)



<a id="examples"></a>
## EXAMPLE


Below is an example of running an uninstall dry run on a client. Nothing is change on the system 
except that it is showing you what it would have done, if your ran it with the option '-y'. If you 
really want to uninstall SADMIN, use the 'y' option (sadm_uninstall.sh -y).
{: .text-justify}

### Uninstalling a SADMIN client

```bash
# sadm_uninstall.sh 
================================================================================
Fri May 21 11:38:38 EDT 2021 - sadm_uninstall.sh V1.9 - SADM Lib. V3.70
Server Name: raspi4.maison.ca - Type: LINUX
UBUNTU 20.04 Kernel 5.4.0-1035-raspi
==================================================
 
Dry Run activated
Use '-y' to really remove 'SADMIN' from this system

Uninstalling a SADMIN client.
Removing client crontab file /etc/cron.d/sadm_client ...
Removing profile script /etc/profile.d/sadmin.sh ...
if [ -f /etc/sudoers.d/033_sadmin-nopasswd ] 
    then Removing 'sadmin' user sudo file /etc/sudoers.d/033_sadmin-nopasswd ...
fi 
if [ -f /etc/sudoers.d/033_sadmin ] 
    then Removing 'sadmin' user sudo file /etc/sudoers.d/033_sadmin ...
fi 
Removing sadmin user 'sadmin' ...
Removing sadmin group 'sadmin' ...
Removing 'SADMIN' line in /etc/environment ...
Removing directory structure /opt/sadmin ...
Uninstall of SADMIN client completed.

==================================================
Script exit code is 0 (Success) and execution time is 00:00:44
History ($SADMIN/dat/rch/raspi4_sadm_uninstall.rch) trim to 35 lines($SADM_MAX_RCLINE=35)
Script will send an alert only when it terminate with error ($SADM_ALERT_TYPE=1).
Script succeeded, no alert will be send to 'default' alert group.
New log (/opt/sadmin/log/raspi4_sadm_uninstall.log) created ($SADM_LOG_APPEND='N').
End of sadm_uninstall.sh - Fri May 21 11:38:41 EDT 2021
================================================================================
```

### Uninstalling a SADMIN server

When uninstalling a SADMIN server, more thing need to be done, every steps that would have been 
done are show to the user. Again, if you really want to uninstall a SADM server then use the 
comme line option 'y' (sadm_uninstall.sh -y).   
Below is an output on the screen when we really happen when we delete the SADMIN server version, 
using the '-y' option. Be sure that when you run the uninstall script with the '-y' you are outside
the $SADMIN directory, so it can be removed properly.
{: .text-justify}

```bash
# cd /tmp  (run the uninstall from outside $SADMIN directory)
# sadm_uninstall.sh -y
================================================================================
Sat 22 May 2021 09:56:50 AM EDT - sadm_uninstall.sh V1.9 - SADM Lib. V3.70
Server Name: ubuntu2104.maison.ca - Type: LINUX
UBUNTU 21.04 Kernel 5.11.0-17-generic
==================================================
 
This will remove 'SADMIN Server' from this system, Are you sure [y,n] ? y

Uninstalling a SADMIN server.
Enter MySQL root password (to delete sadmin database or 'q' to Quit) : 
Verifying access to Database ... 
Database access confirmed ...
Removing backup crontab file /etc/cron.d/sadm_backup ...
Removing client crontab file /etc/cron.d/sadm_client ...
Removing server crontab file /etc/cron.d/sadm_server ...
Removing osupdate crontab file /etc/cron.d/sadm_osupdate ...
Removing profile script /etc/profile.d/sadmin.sh ...
Removing 'sadmin' user sudo file /etc/sudoers.d/033_sadmin-nopasswd ...
Removing sadmin user 'sadmin' ...
Making sure database is up ...
Removing database user 'squery' ...
Removing database user 'sadmin' ...
Dropping 'sadmin' database ...
Removing 'SADMIN' line in /etc/hosts
Removing 'SADMIN' line in /etc/environment ...
Removing directory structure /opt/sadmin ...
Uninstall of SADMIN server completed.
root@ubuntu2104:/opt/sadmin# 
```

[Back to the top](#top_of_page)


{% include {{ site.section_options     }} %}
| **-y** | Really remove SADMIN from this system | 

{% include {{ site.section_environment }} %}

{% include {{ site.section_exitcode    }} %}

{% include {{ site.section_author      }} %}

{% include {{ site.section_copyright   }} %}


<a id="seealso"></a>
## SEE ALSO

[sadm_requirements.sh]({% post_url 2019-03-21-sadm-requirements %}) - List/install required SADMIN tools packages  
[SADMIN installation](/_pages/install) - SADMIN installation page  
[sadm_uninstall.sh]({% post_url 2021-05-21-sadm-uninstall %}) - Uninstall the SADMIN tools

