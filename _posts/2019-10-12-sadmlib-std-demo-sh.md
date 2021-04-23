---
title:          sadmlib_std_demo.sh
layout:         single
date_created:   2021-03-16
date_updated:   2021-03-16 
paginate:       false
show_excerpts:  false
entries_layout: list
tags:               [ libraries ]
categories:         [ libraries ] 
author_profile: false
toc:            false
classes:        wide
coll_name:      sadmlib_std_demo.sh
coll_desc:      Demonstrate SADM Bash Shell Library usage
coll_cat:       "SADMIN Utilities Scripts" 
---

O/S : Aix, Linux, MacOS
 
NAME

sadmlib_std_demo.sh   -   SADMIN standard shell library demonstrator, show global variables and functions you can use within your script, with examples.
 
SYNOPSIS

sadmlib_std_demo.sh usage:     [ -v -h -p -s -t  ]    [ -d   0-9  ]   
 
DESCRIPTION

    Show all Library global variables and functions examples, that you can use within your shell script.
    We suggest running this script and pipe the output to 'less' to see how variables and functions works on your system.
        $ sudo $SADMIN/bin/sadmlib_std_demo.sh | less
    Examples below have different values than on your system and that's normal.
    For example, you may have installed SADMIN in '/opt/sadmin' instead of '/sadmin' like below.
    There is a PDF with the output of this script, you can use it for reference purpose.


    User Variables that affect SADMIN Shell Library behavior.


        ====================================================================================================
        sadmlib_std_demo.sh v3.13 - Library v3.02
        User Var. that affect SADMIN behavior  Description                           This System Result             
        ====================================================================================================
        [001] $SADM_VER                        Script Version Number               : 3.13                           
        [002] $SADM_PN                         Script Name                         : sadmlib_std_demo.sh            
        [003] $SADM_INST                       Script Name Without Extension       : sadmlib_std_demo               
        [004] $SADM_USERNAME                   Current User Name                   : root                           
        [005] $SADM_TPID                       Current Process ID                  : 26992                          
        [006] $SADM_MULTIPLE_EXEC              Allow running multiple copy         : Y                              
        [007] $SADM_USE_RCH                    Gen. entry in .rch file             : N                              
        [008] $SADM_LOG_TYPE                   Set Output to [S]creen [L]og [B]oth : B                              
        [009] $SADM_LOG_APPEND                 Append Log or Create New One        : N                              
        [010] $SADM_LOG_HEADER                 Generate Header in log              : N                              
        [011] $SADM_LOG_FOOTER                 Generate or not Footer in log       : N                              
        [012] $SADM_EXIT_CODE                  Script Exit Return Code             : 0                        
        


    SADMIN Shell Library functions available to your script.


        ====================================================================================================
        sadmlib_std_demo.sh v3.16 - Library v3.20
        Calling Functions                      Description                           This System Result
        ====================================================================================================
        [001] $(sadm_get_release)              SADMIN Release Number (XX.XX)       : 1.2.0
        [002] $(sadm_get_ostype)               OS Type (Uppercase,LINUX,AIX,DARWIN): LINUX
        [003] $(sadm_get_osversion)            Return O/S Version (Ex: 7.2, 6.5)   : 7.7.1908
        [004] $(sadm_get_osmajorversion)       Return O/S Major Version (Ex 7, 6)  : 7
        [005] $(sadm_get_osminorversion)       Return O/S Minor Version (Ex 2, 3)  : 7
        [006] $(sadm_get_osname)               O/S Name (REDHAT,CENTOS,UBUNTU,...) : CENTOS
        [007] $(sadm_get_oscodename)           O/S Project Code Name               : Core
        [008] $(sadm_get_kernel_version)       O/S Running Kernel Version          : 3.10.0-1062.4.1.el7.x86_64
        [009] $(sadm_get_kernel_bitmode)       O/S Kernel Bit Mode (32 or 64)      : 64
        [010] $(sadm_get_hostname)             Current Host Name                   : holmes
        [011] $(sadm_get_host_ip)              Current Host IP Address             : 192.168.1.12
        [012] $(sadm_get_domainname)           Current Host Domain Name            : maison.ca
        [013] $(sadm_get_fqdn)                 Fully Qualified Domain Host Name    : holmes.maison.ca
        [014] $(sadm_get_epoch_time)           Get Current Epoch Time              : 1574606133
        [015] $(sadm_epoch_to_date 1574606133) Convert epoch time to date          : 2019.11.24 09:35:33
            WDATE='2019.11.24 09:35:33'
        [016] $(sadm_date_to_epoch "$WDATE")   Convert Date to epoch time          : 1574606133
            DATE1='2016.01.30 10:00:44'
            DATE2='2016.01.30 10:00:03'
        [017] $(sadm_elapse "$DATE1" "$DATE2") Elapse Time between two timestamps  : 00:00:41
        [018] $(sadm_get_packagetype)          Get package type (rpm,deb,aix,dmg)  : rpm

        ====================================================================================================
        sadmlib_std_demo.sh v3.16 - Library v3.20
        SADMIN BASH SHELL SPECIFIC FUNCTIONS   Description                           This System Result
        ====================================================================================================
        [001] $(sadm_server_type)              Host is Physical or Virtual (P/V)   : P
        [002] $(sadm_server_model)             Server model (Ex: HP ProLiant DL580): OptiPlex 7020
        [003] $(sadm_server_serial)            Server serial number (Ex: 4S7GYF1)  : BJSV942
        [004] $(sadm_server_memory)            Server total memory in MB (Ex: 3790): 7729
        [005] $(sadm_server_hardware_bitmode)  CPU Hardware capable of 32/64 bits  : 64
        [006] $(sadm_server_nb_logical_cpu)    Number of Logical CPU on server     : 4
        [007] $(sadm_server_nb_cpu)            Number of Physical CPU on server    : 1
        [008] $(sadm_server_arch)              System Architecture                 : x86_64
        [009] $(sadm_server_nb_socket)         Number of socket on server          : 1
        [010] $(sadm_server_core_per_socket)   Number of Core per Socket           : 4
        [011] $(sadm_server_thread_per_core)   Number of Thread per Core           : 1
        [012] $(sadm_server_cpu_speed)         Server CPU Speed in MHz             : 3500
        [013] $(sadm_server_disks)             Disks list(MB) (DISKNAME|SIZE,...)  : sda|512000,sdb|1024000
        [014] $(sadm_server_vg)                VG list(MB) (VGNAME|SIZE|USED|FREE) : rootvg|476426|449526|26900
        [015] $(sadm_server_ips)               Network IP(Name|IP|Netmask|MAC)     : em1|192.168.1.12|255.255.255.0|98:90:96:b7:64:a2,em1:1|192.168.1.20|255.255.255.0|98:90:96:b7:64:a2,em1:2|192.168.1.68|255.255.255.0|98:90:96:b7:64:a2,em1:3|192.168.1.13|255.255.255.0|98:90:96:b7:64:a2,em1:4|192.168.1.6|255.255.255.0|98:90:96:b7:64:a2,em1:5|192.168.1.23|255.255.255.0|98:90:96:b7:64:a2,em1:6|192.168.1.126|255.255.255.0|98:90:96:b7:64:a2,em1:7|192.168.1.28|255.255.255.0|98:90:96:b7:64:a2,em1:8|192.168.1.43|255.255.255.0|98:90:96:b7:64:a2
        [016] sadm_toupper string              Return string uppercase             : STRING
        [017] sadm_tolower STRING              Return string lowercase             : string
        


    Overview of SADMIN Library 'sadm_start' and 'sadm_stop' function.


        ====================================================================================================
        sadmlib_std_demo.sh v3.13 - Library v3.02
        Overview of sadm_start and sadm_stop function                                                                     
        ====================================================================================================
        Example of utilization:

        # sadm_start                                         # Init Env Dir & RC/Log File
        # if [ $? -ne 0 ] ; then sadm_stop 1 ; exit 1 ;fi    # Exit if Problem
        # main_process                                       # Main Process
        # SADM_EXIT_CODE=$?                                  # Save Error Code
        # sadm_stop $SADM_EXIT_CODE                          # Close SADM Tool & Upd RCH
        # exit $SADM_EXIT_CODE                               # Exit With Global Err (0/1)

        sadm_start
            Start and initialize sadm environment - Accept no Parameter
            If SADMIN root directory is not /sadmin, make sure the SADMIN Env. variable is set to proper dir.
            Please call this function when your script is starting
            What this function will do for us :
                1) Make sure all directories & sub-directories exist and have proper permissions.
                2) Make sure log file exist with proper permission (/sadmin/log/holmes_sadmlib_std_demo.log)
                3) Make sure Return Code History (.rch) exist and have the right permission
                4) If PID file exist, show error message and abort.
                Unless user allow more than one copy to run simultaniously (SADM_MULTIPLE_EXEC='Y')
                1) Add line in the [R]eturn [C]ode [H]istory file stating script is started (Code 2)
                2) Write HostName - Script name and version - O/S Name and version to the Log file (SADM_LOG)

        sadm_stop
            Accept one parameter - Either 0 (Successfull) or non-zero (Error Encountered)
            Please call this function just before your script end
            What this function do.
                1) If Exit Code is not zero, change it to 1.
                2) Get Actual Time and Calculate the Execution Time.
                3) Writing the Script Footer in the Log (Script Return code, Execution Time, ...)
                4) Update the RCH File (Start/End/Elapse Time and the Result Code)
                5) Trim The RCH File Based on User choice in sadmin.cfg
                6) Write to Log the user mail alerting type choose by user (sadmin.cfg)
                7) Trim the Log based on user selection in sadmin.cfg
                8) Send Email to sysadmin (if user selected that option in sadmin.cfg)
                9) Delete the PID File of the script (SADM_PID_FILE)
            1)  Delete the User 3 TMP Files (SADM_TMP_FILE1, SADM_TMP_FILE2, SADM_TMP_FILE3)
         


    All variables content of the SADMIN configuration file are also accessible in your script.


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
        


    There is also a set a variables that you can use in your script to access SADMIN Directories.


        ====================================================================================================
        sadmlib_std_demo.sh v3.13 - Library v3.02
        Client Directories Var. Avail.         Description                           This System Result             
        ====================================================================================================
        [001] $SADM_BASE_DIR                   SADMIN Root Directory               : /sadmin                        
        [002] $SADM_BIN_DIR                    SADMIN Scripts Directory            : /sadmin/bin                    
        [003] $SADM_TMP_DIR                    SADMIN Temporary file(s) Directory  : /sadmin/tmp                    
        [004] $SADM_LIB_DIR                    SADMIN Shell & Python Library Dir.  : /sadmin/lib                    
        [005] $SADM_LOG_DIR                    SADMIN Script Log Directory         : /sadmin/log                    
        [006] $SADM_CFG_DIR                    SADMIN Configuration Directory      : /sadmin/cfg                    
        [007] $SADM_SYS_DIR                    Server Startup/Shutdown Script Dir. : /sadmin/sys                    
        [008] $SADM_DOC_DIR                    SADMIN Documentation Directory      : /sadmin/doc                    
        [009] $SADM_PKG_DIR                    SADMIN Packages Directory           : /sadmin/pkg                    
        [010] $SADM_DAT_DIR                    Server Data Directory               : /sadmin/dat                    
        [011] $SADM_NMON_DIR                   Server NMON - Data Collected Dir.   : /sadmin/dat/nmon               
        [012] $SADM_DR_DIR                     Server Disaster Recovery Info Dir.  : /sadmin/dat/dr                 
        [013] $SADM_RCH_DIR                    Server Return Code History Dir.     : /sadmin/dat/rch                
        [014] $SADM_NET_DIR                    Server Network Info Dir.            : /sadmin/dat/net                
        [015] $SADM_RPT_DIR                    SYStem MONitor Report Directory     : /sadmin/dat/rpt                
        [016] $SADM_DBB_DIR                    Database Backup Directory           : /sadmin/dat/dbb                
        [017] $SADM_SETUP_DIR                  SADMIN Installation/Update Dir.     : /sadmin/setup                  
        [018] $SADM_USR_DIR                    User/System specific directory      : /sadmin/usr                    
        [019] $SADM_UBIN_DIR                   User/System specific bin/script Dir.: /sadmin/usr/bin                
        [020] $SADM_ULIB_DIR                   User/System specific library Dir.   : /sadmin/usr/lib                
        [021] $SADM_UDOC_DIR                   User/System specific documentation  : /sadmin/usr/doc                
        [022] $SADM_UMON_DIR                   User/System specific SysMon Scripts : /sadmin/usr/mon               

        ====================================================================================================
        sadmlib_std_demo.sh v3.13 - Library v3.02
        Server Directories Var. Avail.         Description                           This System Result             
        ====================================================================================================
        [001] $SADM_WWW_DIR                    SADMIN Web Site Root Directory      : /sadmin/www                    
        [002] $SADM_WWW_DOC_DIR                SADMIN Web Documentation Dir.       : /sadmin/www/doc                
        [003] $SADM_WWW_DAT_DIR                SADMIN Web Site Systems Data Dir.   : /sadmin/www/dat                
        [004] $SADM_WWW_LIB_DIR                SADMIN Web Site PHP Library Dir.    : /sadmin/www/lib                
        [005] $SADM_WWW_TMP_DIR                SADMIN Web Temp Working Directory   : /sadmin/www/tmp                
        [006] $SADM_WWW_PERF_DIR               SADMIN Web Performance Graph Dir.   : /sadmin/www/tmp/perf          
        


    There is also a set a variables that you can use in your script to access SADMIN Files.


        ====================================================================================================
        sadmlib_std_demo.sh v3.13 - Library v3.02
        SADMIN FILES VARIABLES AVAIL.          Description                           This System Result             
        ====================================================================================================
        [001] $SADM_PID_FILE                   Current script PID file             : /sadmin/tmp/sadmlib_std_demo.pid
        [002] $SADM_CFG_FILE                   SADMIN Configuration File           : /sadmin/cfg/sadmin.cfg         
        [003] $SADM_CFG_HIDDEN                 SADMIN Initial Configuration File   : /sadmin/cfg/.sadmin.cfg        
        [004] $SADM_ALERT_FILE                 SADMIN Alert Group File             : /sadmin/cfg/alert_group.cfg    
        [005] $SADM_ALERT_INIT                 SADMIN Initial Alert Group File     : /sadmin/cfg/.alert_group.cfg   
        [006] $SADM_SLACK_FILE                 SADMIN Slack Channel WebHook File   : /sadmin/cfg/alert_slack.cfg    
        [007] $SADM_SLACK_INIT                 SADMIN Initial Slack WebHook File   : /sadmin/cfg/.alert_slack.cfg   
        [008] $SADM_ALERT_HIST                 SADMIN Alert History File           : /sadmin/cfg/alert_history.txt  
        [009] $SADM_ALERT_HINI                 SADMIN Initial Alert History File   : /sadmin/cfg/.alert_history.txt 
        [010] $SADM_ALERT_SEQ                  SADMIN Alert Reference Number File  : /sadmin/cfg/alert_history.seq  
        [011] $SADM_TMP_FILE1                  User usable Temp Work File 1        : /sadmin/tmp/sadmlib_std_demo_1.26992
        [012] $SADM_TMP_FILE2                  User usable Temp Work File 2        : /sadmin/tmp/sadmlib_std_demo_2.26992
        [013] $SADM_TMP_FILE3                  User usable Temp Work File 3        : /sadmin/tmp/sadmlib_std_demo_3.26992
        [014] $SADM_LOG                        Script Log File                     : /sadmin/log/holmes_sadmlib_std_demo.log
        [015] $SADM_RCHLOG                     Script Return Code History File     : /sadmin/dat/rch/holmes_sadmlib_std_demo.rch
        [016] $DBPASSFILE                      SADMIN Database User Password File  : /sadmin/cfg/.dbpass            
        [017] $SADM_RPT_FILE                   SYStem MONitor Report File          : /sadmin/dat/rpt/holmes.rpt     
        [018] $SADM_BACKUP_LIST                Backup List File Name               : /sadmin/cfg/backup_list.txt    
        [019] $SADM_BACKUP_LIST_INIT           Initial Backup List (Template)      : /sadmin/cfg/.backup_list.txt   
        [020] $SADM_BACKUP_EXCLUDE             Backup Exclude List File Name       : /sadmin/cfg/backup_exclude.txt 
        [021] $SADM_BACKUP_EXCLUDE_INIT        Initial Backup Exclude (Template)   : /sadmin/cfg/.backup_exclude.txt   
        


    All these variables are filled automatically when you call the 'sadm_start' function.


        ====================================================================================================
        sadmlib_std_demo.sh v3.13 - Library v3.02
        COMMAND PATH USE BY SADMIN STD. LIBR.  Description                           This System Result             
        ====================================================================================================
        [001] $SADM_LSB_RELEASE                Cmd. 'lsb_release', Get O/S Version : /bin/lsb_release               
        [002] $SADM_DMIDECODE                  Cmd. 'dmidecode', Get model & type  : /sbin/dmidecode                
        [003] $SADM_FACTER                     Cmd. 'facter', Get System Info      : /bin/facter                    
        [004] $SADM_BC                         Cmd. 'bc', Do some Math.            : /bin/bc                        
        [005] $SADM_FDISK                      Cmd. 'fdisk', Get Partition Info    : /sbin/fdisk                    
        [006] $SADM_WHICH                      Cmd. 'which', Get Command location  : /bin/which                     
        [007] $SADM_PERL                       Cmd. 'perl', epoch time Calc.       : /bin/perl                      
        [008] $SADM_MAIL                       Cmd. 'mail', Send SysAdmin Email    : /bin/mail                      
        [009] $SADM_MUTT                       Cmd. 'mutt', Used to Send Email     : /bin/mutt                      
        [010] $SADM_CURL                       Used to send alert to Slack         : /bin/curl                      
        [011] $SADM_LSCPU                      Cmd. 'lscpu', Socket & thread info  : /bin/lscpu                     
        [012] $SADM_NMON                       Cmd. 'nmon', Collect Perf Statistic : /bin/nmon                      
        [013] $SADM_PARTED                     Cmd. 'parted', Get Disk Real Size   : /sbin/parted                   
        [014] $SADM_ETHTOOL                    Cmd. 'ethtool', Get System IP Info  : /sbin/ethtool                  
        [015] $SADM_SSH                        Cmd. 'ssh', SSH to SADMIN client    : /bin/ssh                       
        [016] $SADM_SSH_CMD                    Cmd. 'ssh', SSH to Connect to client: /bin/ssh -qnp32                 
        

    If variable content is blank, it means that the command is not available on the current system. 


 
OPTIONS

-p
    Show database password on output.
-s
    Show Storix Backup information.
-t
    Show TextBelt API Key
-d
    Specify debug level (0-9).
    Value of 0 indicate that no debug information is to be displayed.
-h
    Display this help and exit.
-v
    Output version information and exit.



REQUIREMENTS

    Environment variable 'SADMIN', specify the root directory of the SADMIN tools.
    Define by setup script in /etc/profile.d/sadmin.sh and in /etc/environment .
    SADMIN main configuration file, "$SADMIN/cfg/sadmin.cfg"
    SADMIN Tools Shell Library, "$SADMIN/lib/sadmlib.sh".


 
EXIT STATUS
[0]    An exit status of zero indicates success
[1]    Failure is indicated by a nonzero value, typically ‘1’.

 
AUTHOR
Jacques Duplessis (jacques.duplessis@sadmin.ca.).
Any suggestions or bug report can be sent at http://www.sadmin.ca/support.php

 
COPYRIGHT
Copyright © 2020 Free Software Foundation, Inc. License GPLv3+:
    - GNU GPL version 3 or later http://gnu.org/licenses/gpl.html.
This is free software, you are free to change and redistribute it.
There is NO WARRANTY to the extent permitted by law.

 
SEE ALSO
sadm_template.sh    - Using the SADMIN Shell Template (sadm_template.sh)
sadm_template.py    - Using the SADMIN Python Template (sadm_template.py)
sadm_template_menu.sh    - Using the SADMIN Shell Menu Building Template (sadm_template_menu.sh)
sadm_wrapper.sh    - Use this wrapper to call your existing scripts and benefit of SADMIN tools.
sadmlib_std_demo.sh    - Show all global variables and functions you can use within your shell script, with examples.
sadmlib_std_demo.py    - Show all global variables and functions/modules you can use within your Python script, with examples.

 
INDEX

NAME
SYNOPSIS
DESCRIPTION
OPTIONS
REQUIREMENTS
EXIT STATUS
AUTHOR
COPYRIGHT
SEE ALSO