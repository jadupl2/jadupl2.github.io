---
title:          sadm_support_request.sh
desc:           Create a file that will help us, when you submit a problem.
version:        2.2
updated:        2021-05_04
os:             Linux, Aix, MacOS 
type:           B  # [S]=Run on Server only, [C]=Client Only, [B]=Run on Both
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

<font size="3">
<div>$SADMIN/bin/{{ page.title }}</div>
<div>Version v{{ page.version }} - 
Posted {{ page.date | date: "%Y-%m-%d" }} - 
Updated {{ page.updated }}</div>
<div>Run on {{ page.os }}</div>
</font>



<a id="name"></a>

## NAME
{{ page.title }} -- {{ page.desc }}


<a id="synopsis"></a>  
## SYNOPSIS

```bash
{{ page.title }} [-v] [-h] [-d 0-9]  
```
{% if page.type == "S" %}
<font size="3">Can only be run on SADMIN Server.</font>
{% endif %}



<a id="description"></a>

## DESCRIPTION

This script is use to create a file that contain information that will help us, when you submit 
a problem. When you submit a problem or request support it is important to attach the file 
produced by this script to your email.
{: .text-justify}
 


<a id="examples"></a>

## EXAMPLE

```bash
root@borg:/etc/cron.d  # sadm_support_request.sh 
================================================================================
Mon 26 Apr 2021 08:55:49 AM EDT - sadm_support_request.sh V2.2 - SADM Lib. V3.69
Server Name: borg.maison.ca - Type: LINUX
UBUNTU 20.04 Kernel 5.8.0-50-generic
==================================================
 
Adding /etc/environment to support request log ...
Adding /etc/profile.d/sadmin.sh to support request log ...
Adding /opt/sadmin/cfg/sadmin.cfg to support request log ...
Adding /etc/sudoers.d/033_sadmin-nopasswd to support request log ...
Adding /etc/cron.d/sadm_client to support request log ...
Adding /etc/postfix/main.cf to support request log ...
Adding /etc/hosts to support request log ...
Adding /opt/sadmin/dat/dr/borg_sysinfo.txt to support request log ...

Running /opt/sadmin/bin/sadmlib_std_demo.sh ...
[SUCCESS] Script sadmlib_std_demo.sh terminated.
Adding /opt/sadmin/tmp/borg_sadmlib_std_demo.log to support request log ...

Running /opt/sadmin/bin/sadmlib_std_demo.py ...
[SUCCESS] Script sadmlib_std_demo.py terminated.
Adding /opt/sadmin/tmp/borg_sadmlib_std_demo.log to support request log ...

Running /opt/sadmin/bin/sadm_requirements.sh ...
[SUCCESS] Script sadm_requirements.sh terminated.
Adding /opt/sadmin/tmp/borg_sadm_requirements.sh.log to support request log ...

Running chage -l sadmin ...
Adding /opt/sadmin/tmp/borg_chage.log to support request log ...
Recording /opt/sadmin tree structure list in /opt/sadmin/log/borg_sadm_support_tree.log ...
Creating a listing of all files in /opt/sadmin to /opt/sadmin/log/borg_sadm_support_files_list.log ...

==================================================
Script exit code is 0 (Success) and execution time is 00:00:21
Script will send an alert only when it terminate with error ($SADM_ALERT_TYPE=1).
Script succeeded, no alert will be send to 'default' alert group.
New log (/opt/sadmin/log/borg_sadm_support_request.log) created ($SADM_LOG_APPEND='N').
End of sadm_support_request.sh - Mon 26 Apr 2021 08:56:04 AM EDT
================================================================================

Please send the file '/opt/sadmin/tmp/borg_sadm_support_request.tgz' to sadmlinux@gmail.com.
We will get back to you as soon as possible.
```


{% include {{ site.section_options     }} %}

{% include {{ site.section_environment }} %}

{% include {{ site.section_exitcode    }} %}

{% include {{ site.section_author      }} %}

{% include {{ site.section_copyright   }} %}


<a id="seealso"></a>

## SEE ALSO
List SADMIN requirements - [sadm_requirements.sh]({% post_url 2019-03-21-sadm-requirements %})
