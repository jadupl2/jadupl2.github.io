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


## SADMIN installation related

| Link to ...                                                                       | Script | Description  
| :---                                                                              | :---   | :---
| [How-to install SADMIN](/_pages/install)                                          | [setup.sh/sadm_setup.py](/_pages/install)         | SADMIN installation page  
| [How-to uninstall SADMIN]({% post_url 2021-05-21-sadm-uninstall %})               | [sadm_uninstall.sh]({% post_url 2021-05-21-sadm-uninstall %})     | Uninstall procedure page 
| [List/Install SADMIN requirements]({% post_url 2019-03-21-sadm-requirements %})   | [sadm_requirements.sh]({% post_url 2021-05-21-sadm-uninstall %})  | View/Install packages required by SADMIN
| [How-to update client(s)]({% post_url 2021-05-22-sadm-push-sadmin %})                 | [sadm_push_sadmin.sh]({% post_url 2021-05-22-sadm-push-sadmin %})   | Push SADMIN version to one or all actives clients  
| [How-to update SADMIN server]({% post_url 2021-03-14-sadm-update %})                     | Method [1]({% post_url 2021-03-14-sadm-update %}#method1) or [2]({% post_url 2021-03-14-sadm-update %}#method2)         | How-to update to latest version of SADMIN   


## The Web Interface

| Link to ...                                                                 | Description |  
| :---                                                                        | :--- |  
| [How-to add a client]({% post_url 2021-04-11-web-add-client %})             | How-to add a client to SADMIN inventory | 
| [How-to remove a client]({% post_url 2021-05-19-how-to-remove-a-client %})  | How-to remove a client from SADMIN inventory |
| [How-to schedule O/S update](/utilities/sadm-osupdate/#schedule_osupdate)   | Schedule O/S update with Web Interface |
| [How-to schedule a ReaR Image backup]({% post_url 2021-06-12-sadm-rear-backup %}#rear_schedule) | Schedule ReaR backup via theweb interface |


## Utilities

| Link to ...                                                                       | Script | Description  
| :---                                                                              | :---   | :---
| [SADMIN version of 'df' command]({% post_url 2021-06-13-sadm-df %}) | [sdf (sadm_df.sh)]({% post_url 2021-06-13-sadm-df %})  | Customize version of 'df' command
| [View status of all scripts & monitors](/command_line/sadm-show-rch) | [srch (sadm_show_rch.sh)](/command_line/sadm-show-rch) | Show Result History files (.rch) from all systems|
| [SysMon viewer (cmdline)]({% post_url 2021-05-18-sadm-sysmon-tui %})      | [sview (sadm_sysmon_tui.pl)]({% post_url 2021-05-18-sadm-sysmon-tui %}) | System monitor viewer from command line |
| [Support request](/utilities/sadm-support-request) | [sadm_support_request.sh](/utilities/sadm-support-request) | Submit an enhancement or a support request
| [SysAdmin Menu](/utilities/sadm-ui) | [sadm (sadm_ui.sh)](/utilities/sadm-ui) | System Administration Menu | 



## Writing your own scripts   

| Link to ...                                                                       | Script | Description  
| :---                                                                              | :---   | :--- |  
| [Quick-Intro](/_pages/quickstart)                                                 | Templates/Wrapper | Introduction to template & wrapper |
| [How-to use the shell script template]({% post_url 2021-03-16-sadm-template-sh %})| [sadm_template.sh]({% post_url 2021-03-16-sadm-template-sh %}) | Using SADMIN shell script template   
| [How-to use the python template]({% post_url 2021-03-16-sadm-template-py %})      | [sadm_template.py]({% post_url 2021-03-16-sadm-template-py %}) | Using SADMIN python script template    
| [How-to use the menu template]({% post_url 2021-04-30-sadm-template-menu %})      | [sadm_template_menu.sh]({% post_url 2021-04-30-sadm-template-menu %}) | Using SADMIN shell menu template   
| [How-to use the script wrapper]({% post_url 2018-02-11-sadm-wrapper %})           | [sadm_wrapper.sh]({% post_url 2018-02-11-sadm-wrapper %})     | Use the wrapper to run your existing scripts  
| [SADMIN Shell Library Doc.]({% post_url 2021-04-07-sadmlib-std-sh %})                        | [sadmlib_std.sh]({% post_url 2021-04-07-sadmlib-std-sh %}) | SADMIN standard shell library  
| [SADMIN Shell Library Demo]({% post_url 2019-10-12-sadmlib-std-demo-sh %})              | [sadmlib_std_demo.sh]({% post_url 2019-10-12-sadmlib-std-demo-sh %})  | SADMIN Shell library demonstrator   
| [SADMIN Python Library Doc.]({% post_url 2021-04-07-sadmlib-std-py %})                        | [sadmlib_std.py]({% post_url 2021-04-07-sadmlib-std-py %})  | SADMIN standard python library  
| [SADMIN Python Library Demo]({% post_url 2019-10-12-sadmlib-std-demo-py %})              | [sadmlib_std_demo.py]({% post_url 2019-10-12-sadmlib-std-demo-py %})  | SADMIN Python library demonstrator
| [ Library Code Section](/libraries/sadmin-section) | | Minimal code for using SADMIN library |
| [SADMIN Menu Builder Library]({% post_url 2019-10-12-sadmlib-screen-sh %})                  | [sadmlib_screen.sh]({% post_url 2019-10-12-sadmlib-screen-sh %})   | Library use to build shell menu   



## Configuration files

| Name | Location | Description |  
| :--- | :---     | :---
| [SADMIN configuration file]({% post_url 2021-04-26-sadmin-cfg %})| [$SADMIN/cfg/sadmin.cfg]({% post_url 2021-04-26-sadmin-cfg %})                                | SADMIN main configuration file   
| [SysMon configuration file]({% post_url 2021-06-11-sadm-sysmon-config %}) | [$SADMIN/cfg/${HOSTNAME}.smon]({% post_url 2021-06-11-sadm-sysmon-config %}) | System Monitor configuration file |
| [System information file]({% post_url 2021-05-30-sysinfo-file %})| [$SADMIN/dat/dr/$hostname_sysinfo.txt)]({% post_url 2021-05-30-sysinfo-file %}) | Hardware/Software info about system file  



## System Monitor related information

| Link to ...                                                               | Script | Description  
| :---                                                                      | :---   | :--- |   
| [SADMIN System Monitor]({% post_url 2021-06-10-sadm-sysmon %})            | [sadm_sysmon.pl]({% post_url 2021-06-10-sadm-sysmon %})| SADMIN System Monitor (SysMon) |
| [SysMon configuration file]({% post_url 2021-06-11-sadm-sysmon-config %}) | [$SADMIN/cfg/${HOSTNAME}.smon]({% post_url 2021-06-11-sadm-sysmon-config %}) | System Monitor configuration file |
| [SysMon viewer (cmdline)]({% post_url 2021-05-18-sadm-sysmon-tui %})      | [sview (sadm_sysmon_tui.pl)]({% post_url 2021-05-18-sadm-sysmon-tui %}) | System monitor viewer from command line |
| [Pull log,rpt ans rch from clients]({% post_url 2021-03-16-sadm-fetch-client %}) | [sadm_fetch_client.sh]({% post_url 2021-03-16-sadm-fetch-client %})               | Pull .rch/.log/.rpt from actives clients  
| [How-to setup SMS notification](/how-to/how-to-sms) | | How-to use SMS/Texto alerting system 



## Backup scripts

| Link to ...                                                               | Script | Description  
| :---                                                                      | :---   | :--- |   
| [Daily backup script]({% post_url 2021-05-24-sadm-backup %})              | [sadm_backup.sh]({% post_url 2021-05-24-sadm-backup %})   | Backup based on the content of the backup list & exclude file  
| [Save filesystem metadata]({% post_url 2021-06-02-sadm-dr-savefs %}) | [sadm_dr_savefs.sh]({% post_url 2021-06-02-sadm-dr-savefs %}) | Save filesystems metadata (use by [sadm_dr_recreatefs.sh]({% post_url 2021-06-04-sadm-dr-recreatefs %}))
| [Recreate filesystems]({% post_url 2021-06-04-sadm-dr-recreatefs %})     | [sadm_dr_recreatefs.sh]({% post_url 2021-06-04-sadm-dr-recreatefs %})  | Recreate filesystem using data produced by '[sadm_dr_savefs.sh]({% post_url 2021-06-02-sadm-dr-savefs %})'
| [Backup SADMIN database]({% post_url 2021-05-26-sadm-backupdb %}) | [sadm_backupdb.sh]({% post_url 2021-05-26-sadm-backupdb %})                       | Backup one or all MySQL/MariaDB databases 
| [Backup image of a system]({% post_url 2021-06-12-sadm-rear-backup %})| [sadm_rear_backup.sh]({% post_url 2021-06-12-sadm-rear-backup %})|  Create image backup of the system to a NFS server | 




## Run your own script when system start and when it shutdown

| Link to ...                                                               | Script | Description  
| :---                                                                      | :---   | :--- |   
| [Control Startup/Shutdown script]({% post_url 2021-05-23-sadm-service-ctrl %})       | [sadm_service_ctrl.sh]({% post_url 2021-05-23-sadm-service-ctrl %}) | Enable, disable system startup/shutdown script  





## O/S Update Tools

| Link to ...                                                               | Script | Description  
| :---                                                                      | :---   | :--- |   
| [How-to schedule O/S update](/utilities/sadm-osupdate/#schedule_osupdate) |        | Schedule O/S update with Web Interface |
| [Apply O/S update on current system]({% post_url 2021-06-05-sadm-osupdate %})     | [sadm_osupdate.sh]({% post_url 2021-06-05-sadm-osupdate %})         | Perform Operating System update on the current system
| [Apply O/S update on remote system]({% post_url 2021-06-06-sadm-osupdate-starter %}) | [sadm_osupdate_starter.sh]({% post_url 2021-06-06-sadm-osupdate-starter %})       | Run the O/S update to selected remote system   





## SADMIN Client - Daily end of day scripts

| Link to ...                                                               | Script | Description  
| :---                                                                      | :---   | :--- |   
| [Daily end of day script]({% post_url 2021-05-31-sadm-client-sunset %})    | [sadm_client_sunset.sh]({% post_url 2021-05-31-sadm-client-sunset %})          | Main script that run the 4 scripts below|   
| [1. Client housekeeping]({% post_url 2021-05-29-sadm-client-housekeeping %})| [sadm_client_housekeeping.sh]({% post_url 2021-05-29-sadm-client-housekeeping %}) | Purge old log,rch,nmon files and check $SADMIN permission   
| [2. Create sysinfo file]({% post_url 2021-04-22-sadm-create-sysinfo %}) | [sadm_create_sysinfo.sh]({% post_url 2021-04-22-sadm-create-sysinfo %})           | Collect hardware & software information about the system   
| [3. Save filesystem metadata]({% post_url 2021-06-02-sadm-dr-savefs %}) | [sadm_dr_savefs.sh]({% post_url 2021-06-02-sadm-dr-savefs %}) | Save filesystems metadata (use by [sadm_dr_recreatefs.sh]({% post_url 2021-06-04-sadm-dr-recreatefs %}))
| [4. Produce Sysinfo HTML]({% post_url 2021-06-01-sadm-cfg2html %}) | [sadm_cfg2html.sh]({% post_url 2021-06-01-sadm-cfg2html %}) | Get System information and creates a HTML web page of it  





## SADMIN Server - Daily start of day scripts


| Link to ...                                                               | Script | Description  
| :---                                                                      | :---   | :--- |   
| [Daily start of day script]({% post_url 2021-05-26-sadm-server-sunrise %}) | [sadm_server-sunrise.sh]({% post_url 2021-05-26-sadm-server-sunrise %})           | Main script that run the 6 scripts below| 
| [1. Directories housekeeping]({% post_url 2021-05-27-sadm-server-housekeeping %}) | [sadm_server_houskeeping.sh]({% post_url 2021-05-27-sadm-server-housekeeping %})| Enforce security SADMIN Web interface & crontab files
| [2. Collect clients latest data]({% post_url 2021-05-28-sadm-daily-farm-fetch %}) | [sadm_daily_farm_fetch.sh]({% post_url 2021-05-28-sadm-daily-farm-fetch %})       | Collect Hardware/Software/Performance data from clients   
| [3. Update SADMIN database]({% post_url 2021-05-29-sadm-database-update %}) | [sadm_database_update.py]({% post_url 2021-05-29-sadm-database-update %})         | Take SysInfo collected from clients and update database    
| [4. Update perf. database]({% post_url 2021-05-29-sadm-nmon-rrd-update %}) | [sadm_nmon_rrd_update.sh]({% post_url 2021-05-29-sadm-nmon-rrd-update %})         | Daily performance graphic database update   
| [5. Scan selected subnet]({% post_url 2021-05-29-sadm-subnet-lookup %}) | [sadm_subnet-lookup.py]({% post_url 2021-05-29-sadm-subnet-lookup %})             | Scan network selected subnet & store info in database  
| [6. Backup SADMIN database]({% post_url 2021-05-26-sadm-backupdb %}) | [sadm_backupdb.sh]({% post_url 2021-05-26-sadm-backupdb %})                       | Backup SADMIN database
| [Email Sysadmin daily report]({% post_url 2021-04-01-sadm-daily-report %}) | [sadm_daily_report]({% post_url 2021-04-01-sadm-daily-report %})                 | Produce and email monitoring daily reports





## SADMIN Directory structure

![SADMIN Directories Structure](/assets/img/sadmin_directory_structure.png){: .align-center} 

