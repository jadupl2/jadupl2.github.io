---
title:          man_template.sh
desc:           Template for scripts documentation
version:        2.2
updated:        2021-04-22
os:             Linux, Aix, MacOS
type:           C  # [D]oc [S]=Server only [C]=Client [B]oth
tags:           [ test ] 
#categories:     [ how-to, web_interface, backup, configuration_files, system_monitor, server_scripts, client-scripts, command_line,  utilities, libraries, templates, test ] 
categories:     [ test ] 
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

The running scripts are listed first, then the scripts that terminated with an error and 
finally all the scripts grouped by system. So it give you view of the statistics of each script 
(start time, end time, elapse time,...) of each systems sorted and grouped by name. When 
something look different than the normal, like the alert group used is different than the 
default group or the last execution date of a script is more than thirty days, it will be 
shown with a yellow background. 
{: .text-justify}
 
```bash
# include script
```

[Back to the top](#top_of_page)



<a id="examples"></a>
## EXAMPLE

```bash
# Example of script output
```
<!-- ![Daily Script Report Example](/assets/img/man/sadm_daily_report_script.png){: .align-center} -->

[Back to the top](#top_of_page)


{% include {{ site.section_options     }} %}
| **-i** | option -i | 

{% include {{ site.section_environment }} %}

{% include {{ site.section_exitcode    }} %}

{% include {{ site.section_author      }} %}

{% include {{ site.section_copyright   }} %}


<a id="seealso"></a>
## SEE ALSO

[sadm_fetch_client.sh]({% post_url 2021-03-16-sadm-fetch-client %}) - rsync all .rch/.log/.rpt from actives clients to the SADMIN server.  
[sadm_requirements.sh]({% post_url 2019-03-21-sadm-requirements %}) - List/install required SADMIN tools packages  
[sadm_sysmon_tui.pl]({% post_url 2021-05-18-sadm-sysmon-tui %}) -  Command line summary of alerts and failed scripts of all your servers.  
[sadm_daily_report]({% post_url 2021-04-01-sadm-daily-report %}) - Produce and email monitoring daily reports
[sadm_template.sh]({% post_url 2021-03-16-sadm-template-sh %}) - Using SADMIN shell script template   
[sadm_template.py]({% post_url 2021-03-16-sadm-template-py %}) - Using SADMIN python script template    
[sadm_template_menu.sh]({% post_url 2021-04-30-sadm-template-menu %}) - Using SADMIN shell menu template   
[sadm_wrapper.sh]({% post_url 2018-02-11-sadm-wrapper %}) - Use to run your existing scripts & benefit of SADMIN tools  
[sadmlib_std.sh]({% post_url 2021-04-07-sadmlib-std-sh %}) - SADMIN standard shell library  
[sadmlib_std.py]({% post_url 2021-04-07-sadmlib-std-py %}) - SADMIN standard python library  
[sadmlib_screen.sh]({% post_url 2019-10-12-sadmlib-screen-sh %}) - SADMIN screen oriented library  
[sadmlib_std_demo.sh]({% post_url 2019-10-12-sadmlib-std-demo-sh %}) - SADMIN shell library functions demo   
[sadmlib_std_demo.py]({% post_url 2019-10-12-sadmlib-std-demo-py %}) - SADMIN python library functions demo  
[SADMIN installation](/_pages/install) - SADMIN installation page  
[How-to Add a client]({% post_url 2021-04-11-web-add-client %}) - How-to add a client to SADMIN inventory  
[How-to Remove a client]({% post_url 2021-05-19-how-to-remove-a-client %}) - How-to remove a client from SADMIN inventory  
[sadm_uninstall.sh]({% post_url 2021-05-21-sadm-uninstall %}) - Uninstall the SADMIN tools  
[sadm_push_sadmin.sh]({% post_url 2021-05-22-sadm-push-sadmin %}) - Push SADMIN version to one or all actives clients  
[sadm_create_sysinfo.sh]({% post_url 2021-04-22-sadm-create-sysinfo %}) - Collect hardware & software information about the system  
[How-to update SADMIN]({% post_url 2021-03-14-sadm-update %}) - How-to update to latest version of SADMIN   
[sadm_service_ctrl.sh]({% post_url 2021-05-23-sadm-service-ctrl %}) - Enable, Disable and get status of system startup and shutdown script  
[sadm_backup.sh]({% post_url 2021-05-24-sadm-backup %}) - Backup based on the content of the backup list & exclude file  
[sadmin.cfg]({% post_url 2021-04-26-sadmin-cfg %}) - SADMIN main configuration file  

