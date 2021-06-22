---
title:          man_template.sh
desc:           Template for scripts documentation
version:        2.2
summary: |         
    Page under construction, should be completed soon, come back later.
    {: .text-justify}
updated:        2021-04-22
os:             Linux, Aix, MacOS
type:           C  # [D]oc [S]=Server only [C]=Client [B]oth
categories:     [ test ] 
#categories:     [ how-to, web_interface, backup, configuration-files, system_monitor, server-scripts, client-scripts, command_line,  utilities, libraries, templates, test ] 
tags:           [ test ] 
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
{{ page.summary }} 


<a id="name"></a>
## NAME
**{{ page.title }}**  
*{{ page.desc }}*   



<a id="synopsis"></a>
## SYNOPSIS

```bash
{{ page.title }} [-d 0-9] [-h] [-v]
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

{{ page.summary }} 

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

| Link to ...| Description |  
| :--- | :--- |  
| [sadm_requirements.sh]({% post_url 2019-03-21-sadm-requirements %})               | List/install required SADMIN tools packages  
| [sview]({% post_url 2021-05-18-sadm-sysmon-tui %})                   |  Command line summary of alerts and failed scripts of all your servers.  
| [sadm_daily_report]({% post_url 2021-04-01-sadm-daily-report %})                  | Produce and email monitoring daily reports
| [sadm_template.sh]({% post_url 2021-03-16-sadm-template-sh %})                    | Using SADMIN shell script template   
| [sadm_template.py]({% post_url 2021-03-16-sadm-template-py %})                    | Using SADMIN python script template    
| [sadm_template_menu.sh]({% post_url 2021-04-30-sadm-template-menu %})             | Using SADMIN shell menu template   
| [sadm_wrapper.sh]({% post_url 2018-02-11-sadm-wrapper %})                         | Use to run your existing scripts & benefit of SADMIN tools  
| [sadmlib_std.sh]({% post_url 2021-04-07-sadmlib-std-sh %})                        | SADMIN standard shell library  
| [sadmlib_std.py]({% post_url 2021-04-07-sadmlib-std-py %})                        | SADMIN standard python library  
| [sadmlib_screen.sh]({% post_url 2019-10-12-sadmlib-screen-sh %})                  | SADMIN screen oriented library  
| [sadmlib_std_demo.sh]({% post_url 2019-10-12-sadmlib-std-demo-sh %})              | SADMIN shell library functions demo   
| [sadmlib_std_demo.py]({% post_url 2019-10-12-sadmlib-std-demo-py %})              | SADMIN python library functions demo  
| [SADMIN installation](/_pages/install)                                            | SADMIN installation page  
| [How-to Add a client]({% post_url 2021-04-11-web-add-client %})                   | How-to add a client to SADMIN inventory  
| [How-to Remove a client]({% post_url 2021-05-19-how-to-remove-a-client %})        | How-to remove a client from SADMIN inventory  
| [sadm_uninstall.sh]({% post_url 2021-05-21-sadm-uninstall %})                     | Uninstall the SADMIN tools  
| [sadm_push_sadmin.sh]({% post_url 2021-05-22-sadm-push-sadmin %})                 | Push SADMIN version to one or all actives clients  
| [How-to update SADMIN]({% post_url 2021-03-14-sadm-update %})                     | How-to update to latest version of SADMIN   
| [sadm_service_ctrl.sh]({% post_url 2021-05-23-sadm-service-ctrl %})               | Enable, Disable and get status of system startup and shutdown script  
| [sadm_backup.sh]({% post_url 2021-05-24-sadm-backup %})                           | Backup based on the content of the backup list & exclude file  
| [sadmin.cfg]({% post_url 2021-04-26-sadmin-cfg %})                                | SADMIN main configuration file   
| [sadm_server-sunrise.sh]({% post_url 2021-05-26-sadm-server-sunrise %})           | Collect & process data produced by all actives clients  
| [sadm_server_housekeeping.sh]({% post_url 2021-05-27-sadm-server-housekeeping %}) | Enforce security SADMIN Web interface & crontab files
| [sadm_daily_farm_fetch.sh]({% post_url 2021-05-28-sadm-daily-farm-fetch %})       | Collect Hardware/Software/Performance data from actives servers   
| [sadm_database_update.py]({% post_url 2021-05-29-sadm-database-update %})         | Take data collected from clients and update database    
| [sadm_nmon_rrd_update.sh]({% post_url 2021-05-29-sadm-nmon-rrd-update %})         | Daily performance database update   
| [sadm_subnet-lookup.py]({% post_url 2021-05-29-sadm-subnet-lookup %})             | Scan network selected subnet & store info in database  
| [sadm_backupdb.sh]({% post_url 2021-05-26-sadm-backupdb %})                       | Backup one or all MySQL/MariaDB databases on the system  
| [sadm_client_sunset.sh]({% post_url 2021-05-31-sadm-client-sunset %})             | Clients end of day housekeeping and producing system information files  
| [sadm_client_housekeeping.sh]({% post_url 2021-05-29-sadm-client-housekeeping %}) | Purge old log,rch,nmon files and check $SADMIN permission   
| [sadm_create_sysinfo.sh]({% post_url 2021-04-22-sadm-create-sysinfo %})           | Collect hardware & software information about the system   
| [System Information File]({% post_url 2021-05-30-sysinfo-file %})                 | Documentation about the system information file  
| [sadm_dr_savefs.sh]({% post_url 2021-06-02-sadm-dr-savefs %})                     | Save system filesystems information in order to recreate them from scratch.  
| [sadm_dr_recreatefs.sh]({% post_url 2021-06-04-sadm-dr-recreatefs %})             | Used metadata saved by 'sadm_dr_savefs.sh' to recreate host filesystems  
| [sadm_cfg2html.sh]({% post_url 2021-06-01-sadm-cfg2html %})                       | Get System information and creates a HTML web page of it  
| [sadm_osupdate.sh]({% post_url 2021-06-05-sadm-osupdate %})                       | Perform Operating System update on the current server  
| [sadm_osupdate_starter.sh]({% post_url 2021-06-06-sadm-osupdate-starter %})       | Run the O/S update to selected remote system   
| [sadm_sysmon.pl]({% post_url 2021-06-10-sadm-sysmon %})                           | Client system monitor   
| [sadm_fetch_client.sh]({% post_url 2021-03-16-sadm-fetch-client %})               | rsync all .rch/.log/.rpt from actives clients to the SADMIN server  
| [SysMon configuration file]({% post_url 2021-06-11-sadm-sysmon-config %})         | Client System Monitor configuration file     
| [sadm_rear_backup.sh]({% post_url 2021-06-12-sadm-rear-backup %})|   Create image backup of the system to a NFS server |  
| [smon]({% post_url 2021-06-15-sadm-sysmon-cli %})|   Allow you run SysMon and see the report file |   
| [sdf]({% post_url 2021-06-13-sadm-df %})                                          | sadmin version of the 'df' command |  
| [sadm]({% post_url 2021-06-14-sadm-ui %}) | System Administration Tools Menu |   
| [How-to create a Slack workspace]({% post_url 2021-06-16-sadm-create-slack-workspace %}) | | Create a Slack Workspace |  
| [How-to create Slack channel and App.]({% post_url 2021-06-17-sadm-create-slack-channel-and-slack-app %}) | Configure SADMIN to use Slack|  
| [How-to use SADMIN alerting system]({% post_url 2021-06-18-how-to-use-sadmin-alert %}) | Understanding SADMIN alerting system |  



