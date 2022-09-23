---
title:          Documentation
layout:         single
tags:           [ test ] 
categories:     [ test ] 
#
layout:         single
search:         true
author_profile: false
toc:            false
classes:        wide
sidebar:
  title: "Documentation"
  nav: sidebar-manpage
---
<a id="top_of_page"></a>



<a id="install"></a>
## Install, Uninstall and Update SADMIN

| Name ...                                                                       | Script | Description  
| :---                                                                              | :---   | :---
| [How-to install SADMIN](/_pages/install)                                          | [setup.sh/sadm_setup.py](/_pages/install)         | SADMIN installation page  
| [How-to uninstall SADMIN]({% post_url 2021-05-21-sadm-uninstall %})               | [sadm_uninstall.sh]({% post_url 2021-05-21-sadm-uninstall %})     | Uninstall procedure page 
| [List/Install requirements]({% post_url 2019-03-21-sadm-requirements %})   | [sadm_requirements.sh]({% post_url 2021-05-21-sadm-uninstall %})  | View/Install packages required by SADMIN
| [How-to update client(s)]({% post_url 2021-05-22-sadm-push-sadmin %}) | [sadm_push_sadmin.sh]({% post_url 2021-05-22-sadm-push-sadmin %}) | Push SADMIN version to one or all actives clients  
| [How-to update SADMIN server]({% post_url 2021-03-14-sadm-update %}) | Method [1]({% post_url 2021-03-14-sadm-update %}#method1) or [2]({% post_url 2021-03-14-sadm-update %}#method2) | How-to update to latest version of SADMIN|      
| [Directories structure](/assets/img/sadmin_directory_structure.png) | Image | SADMIN Full directories structure |  
| [Support request](/utilities/sadm-support-request) | [sadm_support_request.sh](/utilities/sadm-support-request) | Submit an enhancement or a support request |  

[Back to the top](#top_of_page)


 


<a id="web_interface"></a>
## Using the web interface

| Name ...                                                                                          | Description |  
| :---                                                                                              | :--- |  
| [How-to add a client]({% post_url 2021-04-11-web-add-client %})                                   | How-to add a client to SADMIN inventory | 
| [How-to remove a client]({% post_url 2021-05-19-how-to-remove-a-client %})                        | How-to remove a client from SADMIN inventory |
| [How-to schedule O/S update](/utilities/sadm-osupdate/#schedule_osupdate)                         | Schedule O/S update with Web Interface |
| [How-to schedule a ReaR Image backup]({% post_url 2021-06-12-sadm-rear-backup %}#rear_schedule)   | Schedule ReaR backup via theweb interface |
| [How-to create a daily backup]({% post_url 2021-05-24-sadm-backup %}#backup_schedule)             | Daily backup what you need with custom retention |  

[Back to the top](#top_of_page)




<a id="command_line"></a>
## Command line tools

| Name ...                                                                       | Script | Description  
| :---                                                                              | :---   | :---
| [sdf]({% post_url 2021-06-13-sadm-df %})           | [sadm_df.sh]({% post_url 2021-06-13-sadm-df %})  | Customize version of 'df' command
| [srch](/command_line/sadm-show-rch)                | [sadm_show_rch.sh](/command_line/sadm-show-rch) | Show Result History files (.rch) from all systems|
| [sview]({% post_url 2021-05-18-sadm-sysmon-tui %}) | [sadm_sysmon_tui.pl]({% post_url 2021-05-18-sadm-sysmon-tui %}) | System monitor viewer from command line |
| [sadm](/command_line/sadm-ui)                         | [sadm_ui.sh](/command_line/sadm-ui) | System Administration Menu | 
| [smon]({% post_url 2021-06-15-sadm-sysmon-cli %})  | [sadm_sysmon_cli.sh]({% post_url 2021-06-15-sadm-sysmon-cli %}) | Run SysMon and view the report file and script(s) error(s)|   
| [Startup/Shutdown script]({% post_url 2021-05-23-sadm-service-ctrl %})       | [sadm_service_ctrl.sh]({% post_url 2021-05-23-sadm-service-ctrl %}) | Enable, disable system startup/shutdown script|  

[Back to the top](#top_of_page)





<a id="writing_scripts"></a>
## Writing your own scripts   

| Name ...                                                                          | Script | Description  
| :---                                                                              | :---   | :--- |  
| [Quick-Intro](/_pages/quickstart)                                                 | Templates/Wrapper | Introduction to template & wrapper |
| [How-to use the shell script template]({% post_url 2021-03-16-sadm-template-sh %})| [sadm_template.sh]({% post_url 2021-03-16-sadm-template-sh %}) | Using SADMIN shell script template   
| [How-to use the python template]({% post_url 2021-03-16-sadm-template-py %})      | [sadm_template.py]({% post_url 2021-03-16-sadm-template-py %}) | Using SADMIN python script template    
| [How-to use the menu template]({% post_url 2021-04-30-sadm-template-menu %})      | [sadm_template_menu.sh]({% post_url 2021-04-30-sadm-template-menu %}) | Using SADMIN shell menu template   
| [How-to use the script wrapper]({% post_url 2018-02-11-sadm-wrapper %})           | [sadm_wrapper.sh]({% post_url 2018-02-11-sadm-wrapper %})     | Use the wrapper to run your existing scripts  
| [SADMIN Shell Library Doc.]({% post_url 2021-04-07-sadmlib-std-sh %})             | [sadmlib_std.sh]({% post_url 2021-04-07-sadmlib-std-sh %}) | SADMIN standard shell library  
| [SADMIN Shell Library Demo]({% post_url 2019-10-12-sadmlib-std-demo-sh %})        | [sadmlib_std_demo.sh]({% post_url 2019-10-12-sadmlib-std-demo-sh %})  | SADMIN Shell library demonstrator   
| [SADMIN Python Library v1 Doc.]({% post_url 2021-04-07-sadmlib-std-py %})         | [sadmlib_std.py]({% post_url 2021-04-07-sadmlib-std-py %})            | SADMIN standard python library v1 ***(Depreciated)***
| [SADMIN Python Library v2 Doc.]({% post_url 2022-08-02-sadmlib2-std-py %})        | [sadmlib2_std.py]({% post_url 2022-08-02-sadmlib2-std-py %})          | SADMIN standard python library v2
| [SADMIN Python Library Demo]({% post_url 2019-10-12-sadmlib-std-demo-py %})       | [sadmlib_std_demo.py]({% post_url 2019-10-12-sadmlib-std-demo-py %})  | SADMIN Python library demonstrator
| [ Library Code Section](/libraries/sadmin-section) | Code to include | Minimal code for using SADMIN library |
| [SADMIN Menu Builder Library]({% post_url 2019-10-12-sadmlib-screen-sh %})        | [sadmlib_screen.sh]({% post_url 2019-10-12-sadmlib-screen-sh %})   | Library use to build shell menu   

[Back to the top](#top_of_page)





<a id="config_files"></a>
## Configuration files

| Name | Location | Description |  
| :--- | :---     | :---
| [Main config file]({% post_url 2021-04-26-sadmin-cfg %})| [$SADMIN/cfg/sadmin.cfg]({% post_url 2021-04-26-sadmin-cfg %})                                | SADMIN main configuration file   
| [SysMon config]({% post_url 2021-06-11-sadm-sysmon-config %}) | [$SADMIN/cfg/${HOSTNAME}.smon]({% post_url 2021-06-11-sadm-sysmon-config %}) | System Monitor configuration file |
| [SysInfo file]({% post_url 2021-05-30-sysinfo-file %})| [$SADMIN/dat/dr/$hostname_sysinfo.txt)]({% post_url 2021-05-30-sysinfo-file %}) | Hardware/Software info about system file  
| [Alert Group File]({% post_url 2021-06-19-alert-group-cfg %})| [$SADMIN/cfg/alert_group.cfg)]({% post_url 2021-06-19-alert-group-cfg %}) | Alert group definition file |
| [Slack config]({% post_url 2021-06-22-alert-slack-cfg %})| [$SADMIN/cfg/alert_slack.cfg)]({% post_url 2021-06-22-alert-slack-cfg %}) | Slack group webhook definition file |
| [Server crontab]({% post_url 2021-06-25-etc-crond-sadm-server %})  | [/etc/crontab.d/sadm_server]({% post_url 2021-06-25-etc-crond-sadm-server %})          | Run everything that keep SADMIN running smoothly |   
| [Client crontab]({% post_url 2021-06-25-etc-crond-sadm-client %})  | [/etc/crontab.d/sadm_client]({% post_url 2021-06-25-etc-crond-sadm-client %})            | Collect perf., sysinfo, run sysmon & housekeeping |   

[Back to the top](#top_of_page)







<a id="sysmon"></a>
## System Monitor

View all your servers alerts from the [web interface](/assets/img/sadm_sysmon/sadm_view_sysmon.png) or on the command line using [sview](/assets/img/sadm_sysmon/sadm_sysmon_tui.png).

| Name ...                                                               | Script | Description  
| :---                                                                      | :---   | :--- |  
| [smon]({% post_url 2021-06-15-sadm-sysmon-cli %})| [smon (sadm_sysmon_cli.sh)]({% post_url 2021-06-15-sadm-sysmon-cli %}) | Run SysMon and see the report file|  
| [sview]({% post_url 2021-05-18-sadm-sysmon-tui %})      | [sview (sadm_sysmon_tui.pl)]({% post_url 2021-05-18-sadm-sysmon-tui %}) | Command line SysMon viewer |
| [System Monitor]({% post_url 2021-06-10-sadm-sysmon %}) | [sadm_sysmon.pl]({% post_url 2021-06-10-sadm-sysmon %})| SADMIN System Monitor (SysMon) |
| [System Monitor Watcher]({% post_url 2021-06-25-sadm-nmon-watcher %})            | [sadm_nmon_watcher.sh]({% post_url 2021-06-25-sadm-nmon-watcher %})| System Monitor Watcher |
| [System Monitor config. file]({% post_url 2021-06-11-sadm-sysmon-config %}) | [$SADMIN/cfg/${HOSTNAME}.smon]({% post_url 2021-06-11-sadm-sysmon-config %}) | System Monitor configuration file |
| [Pull log,rpt ans rch from clients]({% post_url 2021-03-16-sadm-fetch-clients %}) | [sadm_fetch_clients.sh]({% post_url 2021-03-16-sadm-fetch-clients %})               | Pull .rch/.log/.rpt from clients  
| [How-to setup SMS notification](/how-to/how-to-sms) | How-to | How-to use SMS alerting system 
| [How-to create a Slack workspace]({% post_url 2021-06-16-sadm-create-slack-workspace %}) | How-to | Creating a Slack Workspace
| [How-to create Slack channel]({% post_url 2021-06-17-sadm-create-slack-channel-and-slack-app %}) | How-to | Configure Slack Channel & App.|
| [How-to use alerting system]({% post_url 2021-06-18-how-to-use-sadmin-alert %}) | How-to |Understanding the alerting system |  

[Back to the top](#top_of_page)






<a id="backup"></a>
## Backups

| Name ...                                                               | Script | Description  
| :---                                                                      | :---   | :--- |   
| [Daily backup script]({% post_url 2021-05-24-sadm-backup %})              | [sadm_backup.sh]({% post_url 2021-05-24-sadm-backup %})   | Backup based on the backup list content |   
| [Save filesystem metadata]({% post_url 2021-06-02-sadm-dr-savefs %})      | [sadm_dr_savefs.sh]({% post_url 2021-06-02-sadm-dr-savefs %}) | Save filesystems metadata (use by [sadm_dr_recreatefs.sh]({% post_url 2021-06-04-sadm-dr-recreatefs %}))
| [Recreate filesystems]({% post_url 2021-06-04-sadm-dr-recreatefs %})      | [sadm_dr_recreatefs.sh]({% post_url 2021-06-04-sadm-dr-recreatefs %})  | Recreate filesystem saved by '[sadm_dr_savefs.sh]({% post_url 2021-06-02-sadm-dr-savefs %})'
| [Backup database]({% post_url 2021-05-26-sadm-backupdb %})         | [sadm_backupdb.sh]({% post_url 2021-05-26-sadm-backupdb %})                       | Backup one or all MySQL/MariaDB databases 
| [Backup image]({% post_url 2021-06-12-sadm-rear-backup %})    | [sadm_rear_backup.sh]({% post_url 2021-06-12-sadm-rear-backup %})|  Create image backup of the system to a NFS server | 

[Back to the top](#top_of_page)





<a id="osupdate"></a>
## O/S Update Tools

| Name ...                                                               | Script | Description  
| :---                                                                      | :---   | :--- |   
| [How-to schedule O/S update](/utilities/sadm-osupdate/#schedule_osupdate) |        | Schedule O/S update with Web Interface |
| [Update current system O/S]({% post_url 2021-06-05-sadm-osupdate %})     | [sadm_osupdate.sh]({% post_url 2021-06-05-sadm-osupdate %})         | Run O/S update on the current system
| [Update O/S on remote system]({% post_url 2021-06-06-sadm-osupdate-starter %}) | [sadm_osupdate_starter.sh]({% post_url 2021-06-06-sadm-osupdate-starter %})       | Run the O/S update to selected remote system   

[Back to the top](#top_of_page)





<a id="daily_server"></a>
## Server daily start of day scripts

| Name ...                                                               | Script | Description  
| :---                                                                      | :---   | :--- |   
| **[Daily start of day script]({% post_url 2021-05-26-sadm-server-sunrise %})** | [sadm_server-sunrise.sh]({% post_url 2021-05-26-sadm-server-sunrise %})           | Main script that run the 6 scripts below| 
| [1. Dir. housekeeping]({% post_url 2021-05-27-sadm-server-housekeeping %})     | [sadm_server_houskeeping.sh]({% post_url 2021-05-27-sadm-server-housekeeping %})| Set permission on Web interface & crontab files |   
| [2. Collect clients data]({% post_url 2021-05-28-sadm-daily-farm-fetch %})     | [sadm_daily_farm_fetch.sh]({% post_url 2021-05-28-sadm-daily-farm-fetch %})       | Collect Hard./Soft./Perf. data from clients   
| [3. Update database]({% post_url 2021-05-29-sadm-database-update %})           | [sadm_database_update.py]({% post_url 2021-05-29-sadm-database-update %})         | Update database using Sysinfo file |       
| [4. Update perf. database]({% post_url 2021-05-29-sadm-nmon-rrd-update %})     | [sadm_nmon_rrd_update.sh]({% post_url 2021-05-29-sadm-nmon-rrd-update %})         | Daily performance graphic database update   
| [5. Scan selected subnet]({% post_url 2021-05-29-sadm-subnet-lookup %})        | [sadm_subnet-lookup.py]({% post_url 2021-05-29-sadm-subnet-lookup %})             | Scan selected subnet & update database  
| [6. Backup SADMIN database]({% post_url 2021-05-26-sadm-backupdb %})           | [sadm_backupdb.sh]({% post_url 2021-05-26-sadm-backupdb %})                       | Backup SADMIN database
| [Email Sysadmin daily report]({% post_url 2021-04-01-sadm-daily-report %})     | [sadm_daily_report]({% post_url 2021-04-01-sadm-daily-report %})                 | Produce and email monitoring daily reports

[Back to the top](#top_of_page)






<a id="daily_client"></a>
## Client daily end of day scripts

| Name ...                                                               | Script | Description  
| :---                                                                      | :---   | :--- |   
| **[Daily end of day script]({% post_url 2021-05-31-sadm-client-sunset %})**    | [sadm_client_sunset.sh]({% post_url 2021-05-31-sadm-client-sunset %})          | Main script that run the 4 scripts below |   
| [1. Client housekeeping]({% post_url 2021-05-29-sadm-client-housekeeping %})| [sadm_client_housekeeping.sh]({% post_url 2021-05-29-sadm-client-housekeeping %}) | Purge old log,rch,nmon files & check permission |   
| [2. Create sysinfo file]({% post_url 2021-04-22-sadm-create-sysinfo %}) | [sadm_create_sysinfo.sh]({% post_url 2021-04-22-sadm-create-sysinfo %})           | Collect hardware & software info about system   
| [3. Save lvm metadata]({% post_url 2021-06-02-sadm-dr-savefs %})      | [sadm_dr_savefs.sh]({% post_url 2021-06-02-sadm-dr-savefs %}) | Save lvm metadata (use by [sadm_dr_recreatefs.sh]({% post_url 2021-06-04-sadm-dr-recreatefs %}))
| [4. Produce Sysinfo HTML]({% post_url 2021-06-01-sadm-cfg2html %}) | [sadm_cfg2html.sh]({% post_url 2021-06-01-sadm-cfg2html %}) | Get Sysinfo & creates HTML page |  

[Back to the top](#top_of_page)

