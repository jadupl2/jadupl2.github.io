---
title:          sadmlib_std_demo.sh
desc:           SADMIN Shell Library Functions Demo
version:        2.2
updated:        2021-05-04
os:             Linux, Aix, MacOS
type:           B  # [S]=Run on Server only, [C]=Client Only, [B]=Run on Both
tags:           [ libraries ]
categories:     [ libraries ] 
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
**{{ page.title }}** - *{{ page.desc }}*   


<a id="synopsis"></a>
## SYNOPSIS

```bash
{{ page.title }} [ -d 0-9 ] [ -h ] [ -p ] [ -s ] [ -t ] [ -v ]
```


<a id="description"></a>
## DESCRIPTION

Show all Library global variables and functions examples, that you can use within your shell 
script. We suggest running this script and pipe the output to 'less' to see how variables and 
functions works on your system.   
{: .text-justify}  

```$ sudo $SADMIN/bin/sadmlib_std_demo.sh | less```


<a id="examples"></a>
## EXAMPLE

Examples below have different values than on your system and that's normal. For example, you 
may have installed SADMIN in '/opt/sadmin' instead of '/sadmin' like below. There is a PDF with 
the output of this script, you can use it for reference purpose.
{: .text-justify}

**User variables that affect SADMIN shell library behavior**
```bash  
==========================================================================================
sadmlib_std_demo.sh v3.13 - Library v3.02
Var. affecting SADMIN behavior  Description                           System Result 
==========================================================================================
[001] $SADM_VER                 Script Version Number               : 3.13               
[002] $SADM_PN                  Script Name                         : sadmlib_std_demo.sh
[003] $SADM_INST                Script Name Without Extension       : sadmlib_std_demo    
[004] $SADM_USERNAME            Current User Name                   : root                
[005] $SADM_TPID                Current Process ID                  : 26992              
[006] $SADM_MULTIPLE_EXEC       Allow running multiple copy         : Y  
[007] $SADM_USE_RCH             Gen. entry in .rch file             : N  
[008] $SADM_LOG_TYPE            Set Output to [S]creen [L]og [B]oth : B  
[009] $SADM_LOG_APPEND          Append Log or Create New One        : N  
[010] $SADM_LOG_HEADER          Generate Header in log              : N  
[011] $SADM_LOG_FOOTER          Generate or not Footer in log       : N 
[012] $SADM_EXIT_CODE           Script Exit Return Code             : 
```

**SADMIN Shell Library functions available to your script**
```bash  
==========================================================================================
sadmlib_std_demo.sh v3.16 - Library v3.20
Calling Functions                      Description                           System Result
==========================================================================================
[01] $(sadm_get_release)              SADMIN Release Number (XX.XX)      : 1.2.0
[02] $(sadm_get_ostype)               OS Type Uppercase(LINUX,AIX,DARWIN): LINUX
[03] $(sadm_get_osversion)            Return O/S Version (Ex: 7.2, 6.5)  : 7.7.1908
[04] $(sadm_get_osmajorversion)       Return O/S Major Version (Ex 7, 6) : 7
[05] $(sadm_get_osminorversion)       Return O/S Minor Version (Ex 2, 3) : 7
[06] $(sadm_get_osname)               O/S Name (REDHAT,CENTOS,UBUNTU,...): CENTOS
[07] $(sadm_get_oscodename)           O/S Project Code Name              : Core
[08] $(sadm_get_kernel_version)       O/S Running Kernel Version :3.10.0-1062.4.1.el7.x86_64
[09] $(sadm_get_kernel_bitmode)       O/S Kernel Bit Mode (32 or 64)     : 64
[10] $(sadm_get_hostname)             Current Host Name                  : holmes
[11] $(sadm_get_host_ip)              Current Host IP Address            : 192.168.1.12
[12] $(sadm_get_domainname)           Current Host Domain Name           : maison.ca
[13] $(sadm_get_fqdn)                 Fully Qualified Domain Host Name   : holmes.maison.ca
[14] $(sadm_get_epoch_time)           Get Current Epoch Time             : 1574606133
[15] $(sadm_epoch_to_date 1574606133) Convert epoch time to date      : 2019.11.24 09:35:33
    WDATE='2019.11.24 09:35:33'
[16] $(sadm_date_to_epoch "$WDATE")   Convert Date to epoch time         : 1574606133
    DATE1='2016.01.30 10:00:44'
    DATE2='2016.01.30 10:00:03'
[17] $(sadm_elapse "$DATE1" "$DATE2") Elapse Time between two timestamps : 00:00:41
[18] $(sadm_get_packagetype)          Get package type (rpm,deb,aix,dmg) : rpm
```

```bash  
==========================================================================================
sadmlib_std_demo.sh v3.16 - Library v3.20
SADMIN BASH SHELL FUNCTIONS          Description                           System Result
==========================================================================================
[01] $(sadm_server_type)             Host is Physical or Virtual (P/V)   : P
[02] $(sadm_server_model)            Server model (Ex: HP ProLiant DL580): OptiPlex 7020
[03] $(sadm_server_serial)           Server serial number (Ex: 4S7GYF1)  : BJSV942
[04] $(sadm_server_memory)           Server total memory in MB (Ex: 3790): 7729
[05] $(sadm_server_hardware_bitmode) CPU Hardware capable of 32/64 bits  : 64
[06] $(sadm_server_nb_logical_cpu)   Number of Logical CPU on server     : 4
[07] $(sadm_server_nb_cpu)           Number of Physical CPU on server    : 1
[08] $(sadm_server_arch)             System Architecture                 : x86_64
[09] $(sadm_server_nb_socket)        Number of socket on server          : 1
[10] $(sadm_server_core_per_socket)  Number of Core per Socket           : 4
[11] $(sadm_server_thread_per_core)  Number of Thread per Core           : 1
[12] $(sadm_server_cpu_speed)        Server CPU Speed in MHz             : 3500
[13] $(sadm_server_disks)            Disks list(MB) (DISKNAME|SIZE,...)  : sda|512000,sdb|1024000
[14] $(sadm_server_vg)               VG list(MB) (VGNAME|SIZE|USED|FREE) : rootvg|476426|449526|26900
[15] $(sadm_server_ips)              Network IP(Name|IP|Netmask|MAC)     : em1|192.168.1.12|255.255.255.0|98:90:96:b7:64
[16] sadm_toupper string             Return string uppercase             : STRING
[17] sadm_tolower STRING             Return string lowercase             : string
```        

**Main function of the Library, the 'sadm_start' and 'sadm_stop' functions**   

```bash
==================================================================================
sadmlib_std_demo.sh v3.13 - Library v3.02
Overview of sadm_start and sadm_stop function                                     
==================================================================================
sadm_start                                         # Init Env Dir & RC/Log File
if [ $? -ne 0 ] ; then sadm_stop 1 ; exit 1 ;fi    # Exit if Problem
main_process                                       # Main Process
SADM_EXIT_CODE=$?                                  # Save Error Code
sadm_stop $SADM_EXIT_CODE                          # Close SADM Tool & Upd RCH
exit $SADM_EXIT_CODE                               # Exit With Global Err (0/1)
```

---

<a id="sadm_start"></a>
### sadm_start()
This function start and initialize sadm environment and accept no parameter. Make sure the SADMIN 
environment variable is set to proper directory. Call this function when your script is starting.  

**What sadm_start() function does**  
1- Make sure all directories & sub-directories exist and have proper permissions.  
2- Make sure log file exist with proper permission (/sadmin/log/holmes_sadmlib_std_demo.log).  
3- Make sure Return Code History (.rch) exist and have the right permission.  
4- If PID file exist, show error message and abort.  
5- Unless user allow more than one copy to run simultaneously (SADM_MULTIPLE_EXEC='Y').  
6- Add line in the [R]eturn [C]ode [H]istory file stating script is started (Code 2).  
7- Write HostName, script name, O/S name and version to the Log file.  

---

<a id="sadm_stop"></a>
### sadm_stop()
The 'sadm_stop' function accept one parameter. The parameter can be either 0 (Successfully) if the
script terminated with success or with a non-zero (Error Encountered) if it terminated with error.
Please call this function just before your script end.

**What sadm_stop() function does**  
1- If Exit Code is not zero, change it to 1.  
2- Get Actual Time and Calculate the Execution Time.  
3- Writing the Script Footer in the Log (Script Return code, Execution Time, ...)  
4- Update the RCH File (Start/End/Elapse Time and the Result Code)  
5- Trim The RCH File Based on User choice in sadmin.cfg  
6- Write to Log the user mail alerting type choose by user (sadmin.cfg)  
7- Trim the Log based on user selection in sadmin.cfg  
8- Send Email to sysadmin (if user selected that option in sadmin.cfg)  
9- Delete the PID File of the script (SADM_PID_FILE)  
10- Delete the User 3 TMP Files (SADM_TMP_FILE1, SADM_TMP_FILE2, SADM_TMP_FILE3)  
 
---


**Variables loaded from the SADMIN configuration file**

```bash
====================================================================================================
sadmlib_std_demo.sh v3.13 - Library v3.02
SADMIN CONFIG FILE VARIABLES           Description                           This System Result             
====================================================================================================
[001] $SADM_SERVER                     SADMIN SERVER NAME (FQDN)           : holmes.maison.ca               
[002] $SADM_HOST_TYPE                  SADMIN [C]lient or [S]erver         : S                              
[003] $SADM_MAIL_ADDR                  SADMIN Administrator Default Email  : duplessis.jacques@gmail.com    
[004] $SADM_ALERT_TYPE                 0=NoMail 1=OnError 2=OnSuccess 3=All: 1                              
[005] $SADM_ALERT_GROUP                Default Alert Group                 : default                        
[006] $SADM_ALERT_REPEAT               Seconds to wait before repeat alert : 21600                          
[007] $SADM_TEXTBELT_URL               TextBelt.com API URL                : https://textbelt.com/text      
[008] $SADM_CIE_NAME                   Your Company Name                   : Your Cie Name                  
[009] $SADM_DOMAIN                     Server Creation Default Domain      : maison.ca                      
[010] $SADM_USER                       SADMIN User Name                    : sadmin                         
[011] $SADM_GROUP                      SADMIN Group Name                   : sadmin                         
[012] $SADM_WWW_USER                   User that Run Apache Web Server     : apache                         
[013] $SADM_WWW_GROUP                  Group that Run Apache Web Server    : apache                         
[014] $SADM_DBNAME                     SADMIN Database Name                : sadmin                         
[015] $SADM_DBHOST                     SADMIN Database Host                : sadmin.maison.ca               
[016] $SADM_DBPORT                     SADMIN Database Host TCP Port       : 3306                           
[017] $SADM_RW_DBUSER                  SADMIN Database Read/Write User     : sadmin                         
[018] $SADM_RW_DBPWD                   SADMIN Database Read/Write User Pwd :                                
[019] $SADM_RO_DBUSER                  SADMIN Database Read Only User      : squery                         
[020] $SADM_RO_DBPWD                   SADMIN Database Read Only User Pwd  :                                
[021] $SADM_RRDTOOL                    RRDTOOL Binary Location             : /bin/rrdtool                   
[022] $SADM_SSH_PORT                   SSH Port to communicate with client : 32                             
[023] $SADM_NMON_KEEPDAYS              Nb. of days to keep nmon perf. file : 40                             
[024] $SADM_RCH_KEEPDAYS               Nb. days to keep unmodified rch file: 60                             
[025] $SADM_LOG_KEEPDAYS               Nb. days to keep unmodified log file: 60                             
[026] $SADM_MAX_RCLINE                 Trim rch file to this max. of lines : 75                             
[027] $SADM_MAX_LOGLINE                Trim log to this maximum of lines   : 500                            
[028] $SADM_NETWORK1                   Network/Netmask 1 inv. IP/Name/Mac  : 192.168.1.0/24                 
[029] $SADM_NETWORK2                   Network/Netmask 2 inv. IP/Name/Mac  :                                
[030] $SADM_NETWORK3                   Network/Netmask 3 inv. IP/Name/Mac  :                                
[031] $SADM_NETWORK4                   Network/Netmask 4 inv. IP/Name/Mac  :                                
[032] $SADM_NETWORK5                   Network/Netmask 5 inv. IP/Name/Mac  :                                
[033] $SADM_MKSYSB_NFS_SERVER          AIX MKSYSB NFS Server IP or Name    : batnfs.maison.ca               
[034] $SADM_MKSYSB_NFS_MOUNT_POINT     AIX MKSYSB NFS Mount Point          : /volume1/mksysb                
[035] $SADM_MKSYSB_BACKUP_TO_KEEP      AIX MKSYSB NFS Backup - Nb. to keep : 2                              
[036] $SADM_REAR_NFS_SERVER            Rear NFS Server IP or Name          : batnas.maison.ca               
[037] $SADM_REAR_NFS_MOUNT_POINT       Rear NFS Mount Point                : /volume1/Linux_DR              
[038] $SADM_REAR_BACKUP_TO_KEEP        Rear NFS Backup - Nb. to keep       : 3                              
[039] $SADM_BACKUP_NFS_SERVER          NFS Backup IP or Server Name        : batnas.maison.ca               
[040] $SADM_BACKUP_NFS_MOUNT_POINT     NFS Backup Mount Point              : /volume1/backup_linux          
[041] $SADM_DAILY_BACKUP_TO_KEEP       Nb. of Daily Backup to keep         : 4                              
[042] $SADM_WEEKLY_BACKUP_TO_KEEP      Nb. of Weekly Backup to keep        : 4                              
[043] $SADM_MONTHLY_BACKUP_TO_KEEP     Nb. of Monthly Backup to keep       : 4                              
[044] $SADM_YEARLY_BACKUP_TO_KEEP      Nb. of Yearly Backup to keep        : 2                              
[045] $SADM_WEEKLY_BACKUP_DAY          Weekly Backup Day (1=Mon,...,7=Sun) : 5                              
[046] $SADM_MONTHLY_BACKUP_DATE        Monthly Backup Date (1-28)          : 1                              
[047] $SADM_YEARLY_BACKUP_MONTH        Month to take Yearly Backup (1-12)  : 12                             
[048] $SADM_YEARLY_BACKUP_DATE         Date to do Yearly Backup(1-DayInMth): 31                             
```



***Variables set to various SADMIN directories**

```bash
=====================================================================================
sadmlib_std_demo.sh v3.13 - Library v3.02
Client Directories Var.      Description                          This System Result 
======================================================================================
[01] $SADM_BASE_DIR          SADMIN Root Directory               : /sadmin           
[02] $SADM_BIN_DIR           SADMIN Scripts Directory            : /sadmin/bin       
[03] $SADM_TMP_DIR           SADMIN Temporary file(s) Directory  : /sadmin/tmp       
[04] $SADM_LIB_DIR           SADMIN Shell & Python Library Dir.  : /sadmin/lib       
[05] $SADM_LOG_DIR           SADMIN Script Log Directory         : /sadmin/log       
[06] $SADM_CFG_DIR           SADMIN Configuration Directory      : /sadmin/cfg       
[07] $SADM_SYS_DIR           Server Startup/Shutdown Script Dir. : /sadmin/sys       
[08] $SADM_DOC_DIR           SADMIN Documentation Directory      : /sadmin/doc       
[09] $SADM_PKG_DIR           SADMIN Packages Directory           : /sadmin/pkg       
[10] $SADM_DAT_DIR           Server Data Directory               : /sadmin/dat       
[11] $SADM_NMON_DIR          Server NMON - Data Collected Dir.   : /sadmin/dat/nmon  
[12] $SADM_DR_DIR            Server Disaster Recovery Info Dir.  : /sadmin/dat/dr    
[13] $SADM_RCH_DIR           Server Return Code History Dir.     : /sadmin/dat/rch   
[14] $SADM_NET_DIR           Server Network Info Dir.            : /sadmin/dat/net   
[15] $SADM_RPT_DIR           SYStem MONitor Report Directory     : /sadmin/dat/rpt   
[16] $SADM_DBB_DIR           Database Backup Directory           : /sadmin/dat/dbb   
[17] $SADM_SETUP_DIR         SADMIN Installation/Update Dir.     : /sadmin/setup     
[18] $SADM_USR_DIR           User/System specific directory      : /sadmin/usr       
[19] $SADM_UBIN_DIR          User/System specific bin/script Dir.: /sadmin/usr/bin   
[20] $SADM_ULIB_DIR          User/System specific library Dir.   : /sadmin/usr/lib   
[21] $SADM_UDOC_DIR          User/System specific documentation  : /sadmin/usr/doc   
[22] $SADM_UMON_DIR          User/System specific SysMon Scripts : /sadmin/usr/mon 
```

```
========================================================================================
sadmlib_std_demo.sh v3.13 - Library v3.02
Server Directories Var.      Description                           This System Result             
========================================================================================
[01] $SADM_WWW_DIR           SADMIN Web Site Root Directory      : /sadmin/www          
[02] $SADM_WWW_DOC_DIR       SADMIN Web Documentation Dir.       : /sadmin/www/doc      
[03] $SADM_WWW_DAT_DIR       SADMIN Web Site Systems Data Dir.   : /sadmin/www/dat      
[04] $SADM_WWW_LIB_DIR       SADMIN Web Site PHP Library Dir.    : /sadmin/www/lib      
[05] $SADM_WWW_TMP_DIR       SADMIN Web Temp Working Directory   : /sadmin/www/tmp      
[06] $SADM_WWW_PERF_DIR      SADMIN Web Performance Graph Dir.   : /sadmin/www/tmp/perf
```



**Set of variables that contains various file name use by SADMIN**

```bash
====================================================================================================
sadmlib_std_demo.sh v3.13 - Library v3.02
SADMIN FILES VARIABLES AVAIL.   Description                           This System Result  
====================================================================================================
[01] $SADM_PID_FILE             Current script PID file            : /sadmin/tmp/sadmlib_std_demo.pid
[02] $SADM_CFG_FILE             SADMIN Configuration File          : /sadmin/cfg/sadmin.cfg         
[03] $SADM_CFG_HIDDEN           SADMIN Initial Configuration File  : /sadmin/cfg/.sadmin.cfg        
[04] $SADM_ALERT_FILE           SADMIN Alert Group File            : /sadmin/cfg/alert_group.cfg    
[05] $SADM_ALERT_INIT           SADMIN Initial Alert Group File    : /sadmin/cfg/.alert_group.cfg   
[06] $SADM_SLACK_FILE           SADMIN Slack Channel WebHook File  : /sadmin/cfg/alert_slack.cfg    
[07] $SADM_SLACK_INIT           SADMIN Initial Slack WebHook File  : /sadmin/cfg/.alert_slack.cfg   
[08] $SADM_ALERT_HIST           SADMIN Alert History File          : /sadmin/cfg/alert_history.txt  
[09] $SADM_ALERT_HINI           SADMIN Initial Alert History File  : /sadmin/cfg/.alert_history.txt 
[10] $SADM_ALERT_SEQ            SADMIN Alert Reference Number File : /sadmin/cfg/alert_history.seq  
[11] $SADM_TMP_FILE1            User usable Temp Work File 1       : /sadmin/tmp/sadmlib_std_demo_1.26992
[12] $SADM_TMP_FILE2            User usable Temp Work File 2       : /sadmin/tmp/sadmlib_std_demo_2.26992
[13] $SADM_TMP_FILE3            User usable Temp Work File 3       : /sadmin/tmp/sadmlib_std_demo_3.26992
[14] $SADM_LOG                  Script Log File                    : /sadmin/log/holmes_sadmlib_std_demo.log
[15] $SADM_RCHLOG               Script Return Code History File    : /sadmin/dat/rch/holmes_sadmlib_std_demo.rch
[16] $DBPASSFILE                SADMIN Database User Password File : /sadmin/cfg/.dbpass            
[17] $SADM_RPT_FILE             SYStem MONitor Report File         : /sadmin/dat/rpt/holmes.rpt     
[18] $SADM_BACKUP_LIST          Backup List File Name              : /sadmin/cfg/backup_list.txt    
[19] $SADM_BACKUP_LIST_INIT     Initial Backup List (Template)     : /sadmin/cfg/.backup_list.txt   
[20] $SADM_BACKUP_EXCLUDE       Backup Exclude List File Name      : /sadmin/cfg/backup_exclude.txt 
[21] $SADM_BACKUP_EXCLUDE_INIT  Initial Backup Exclude (Template)  : /sadmin/cfg/.backup_exclude.txt   
```


**Variables are set automatically when you call the 'sadm_start()' function**

```bash
=========================================================================================
sadmlib_std_demo.sh v3.13 - Library v3.02
COMMAND PATH                    Description                           This System Result
=========================================================================================
[001] $SADM_LSB_RELEASE         Cmd. 'lsb_release', Get O/S Version : /bin/lsb_release
[002] $SADM_DMIDECODE           Cmd. 'dmidecode', Get model & type  : /sbin/dmidecode 
[003] $SADM_FACTER              Cmd. 'facter', Get System Info      : /bin/facter     
[004] $SADM_BC                  Cmd. 'bc', Do some Math.            : /bin/bc      
[005] $SADM_FDISK               Cmd. 'fdisk', Get Partition Info    : /sbin/fdisk  
[006] $SADM_WHICH               Cmd. 'which', Get Command location  : /bin/which   
[007] $SADM_PERL                Cmd. 'perl', epoch time Calc.       : /bin/perl    
[008] $SADM_MAIL                Cmd. 'mail', Send SysAdmin Email    : /bin/mail    
[009] $SADM_MUTT                Cmd. 'mutt', Used to Send Email     : /bin/mutt    
[010] $SADM_CURL                Used to send alert to Slack         : /bin/curl    
[011] $SADM_LSCPU               Cmd. 'lscpu', Socket & thread info  : /bin/lscpu   
[012] $SADM_NMON                Cmd. 'nmon', Collect Perf Statistic : /bin/nmon    
[013] $SADM_PARTED              Cmd. 'parted', Get Disk Real Size   : /sbin/parted 
[014] $SADM_ETHTOOL             Cmd. 'ethtool', Get System IP Info  : /sbin/ethtool
[015] $SADM_SSH                 Cmd. 'ssh', SSH to SADMIN client    : /bin/ssh     
[016] $SADM_SSH_CMD             Cmd. 'ssh', SSH to Connect to client: /bin/ssh -qnp32
```

*If variable content is blank, it means that the command is not available on the current system.*    


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

