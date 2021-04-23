---
title:          sadmlib_std_demo.py
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
coll_name:      sadmlib_std_demo.py
coll_desc:      Demonstrate SADM Python Library usage
coll_cat:       "SADMIN Utilities Scripts" 
---

NAME

sadmlib_std_demo.py   -   SADMIN standard Python library demonstrator, show global variables and functions you can use within your Python script, with examples,
 
SYNOPSIS

sadmlib_std_demo.py     [ -v -h -p -s -t  ]    [ -d   0-9  ]   
 
DESCRIPTION

    Show with examples all global variables and functions/modules you can use within your Python script.
    We suggest running this script and pipe the ouput to 'less' to see how variables and functions works on your system.
        $ sudo $SADMIN/bin/sadmlib_std_demo.py | less
    Examples below may have different result values on your system and that's normal.
    For example, you may have installed in '/opt/sadmin' instead of '/sadmin' like below.
    There is a PDF with the output of this Python script, you can use it for reference purpose.


    User Variables that affect SADMIN Shell Library behavior.


        ====================================================================================================
        sadmlib_std_demo.py v3.6 - Library v3.02
        User Var. that affect SADMIN behavior  Description                           This System Result             
        ====================================================================================================
        [001] st.ver                           Get/Set Script Version Number       : 3.6 
        [002] st.pn                            Get script name                     : sadmlib_std_demo.py 
        [003] st.inst                          Get script name without extension   : sadmlib_std_demo 
        [004] st.username                      Get current user name               : root 
        [005] st.tpid                          Get Current Process ID              : 3843 
        [006] st.multiple_exec                 Get/Set Allow running multiple copy : Y 
        [007] st.use_rch                       Get/Set Gen. entry in .rch file     : False 
        [008] st.log_type                      Set Output to [S]creen [L]og [B]oth : B 
        [009] st.log_append                    Get/Set Append Log or Create New One: False 
        [010] st.log_header                    Get/Set Generate Header in log      : False 
        [011] st.log_footer                    Get/Set Generate Footer in  log     : False 
        [012] st.exit_code                     Get/Set Script Exit Return Code     : 0 
        


    SADMIN Shell Library Modules/Functions available to your script.


        ====================================================================================================
        sadmlib_std_demo.py v3.10 - Library v3.09
        Calling Functions                      Description                           This System Result
        ====================================================================================================
        [001] st.get_release()                 SADMIN Release Number (XX.XX)       : 1.2.0
        [002] st.get_ostype()                  OS Type (Uppercase,LINUX,AIX,DARWIN): LINUX
        [003] st.get_osversion()               Return O/S Version (Ex: 7.2, 6.5)   : 7.7.1908
        [004] st.get_osmajorversion()          Return O/S Major Version (Ex 7, 6)  : 7
        [005] st.get_osminorversion()          Return O/S Minor Version (Ex 2, 3)  : 7
        [006] st.get_osname()                  O/S Name (REDHAT,CENTOS,UBUNTU,...) : CENTOS
        [007] st.get_oscodename()              O/S Project Code Name               : CORE
        [008] st.get_kernel_version()          O/S Running Kernel Version          : 3.10.0-1062
        [009] st.get_kernel_bitmode()          O/S Kernel Bit Mode (32 or 64)      : 64
        [010] st.hostname                      Current Host Name                   : holmes
        [011] st.get_host_ip()                 Current Host IP Address             : 192.168.1.12
        [012] st.get_domainname()              Current Host Domain Name            : maison.ca
        [013] st.get_fqdn()                    Fully Qualified Domain Host Name    : holmes.maison.ca
        [014] st.get_epoch_time()              Get Current Epoch Time              : 1574605872
        [015] st.epoch_to_date(1574605872)     Convert epoch time to date          : 2019.11.24 09:31:12
            WDATE=2019.11.24 09:31:12
        [016] st.date_to_epoch(WDATE)          Convert Date to epoch time          : 1574605872
            DATE1=2018.06.30 10:00:44
            DATE2=2018.06.30 10:00:03
        [017] st.elapse_time(DATE1,DATE2)      Elapse Time between two timestamps  : 00:00:41
        [018] st.get_packagetype()             Get package type (rpm,deb,aix,dmg)  : rpm
        [019] st.get_arch()                    Get system architecture             : x86_64


        ====================================================================================================
        sadmlib_std_demo.py v3.6 - Library v3.02
        SADMIN PYTHON SPECIFIC FUNCTIONS       Description                           This System Result             
        ====================================================================================================
        [001] st.dbsilent                      When DBerror, No ErrMsg (Just ErrNo): False 
        [002] st.usedb                         Script need (Open/Close) Database ? : True 
        [003] st.silentremove('file')          Silent File Del, No Err if not exist: None 
        [004] st.writelog(msg,'nonl'|'bold')   Write Log (nonl=NoNewLine)          : None 
        


    Overview of SADMIN Library 'sadm_start' and 'sadm_stop' function.


        ====================================================================================================
        sadmlib_std_demo.py v3.6 - Library v3.02
        Overview of st.start() & st.stop() function                                                                     
        ====================================================================================================

        ----------
        st = setup_sadmin()
        Example : st = setup_sadmin()    # Setup Var, Load Libr, Create instance, call st.start()
        ----------
            Setup User Var., Load Module, Create Instance, call st.start() and return instance object
            It make sure the SADMIN Environment variable is set to proper dir.
            The module 'setup_sadmin()', need to be called  when your script is starting.
            What this function will do for us :
                1) Make sure all directories & sub-directories exist and have proper permissions.
                2) Make sure log file exist with proper permission (st.log_file)
                3) Make sure Return Code History (.rch) exist and have the right permission
                4) If PID file exist, show error message and abort.
                Unless user allow more than one copy to run simultaneously (st.multiple_exec = 'Y')
                5) Add line in the [R]eturn [C]ode [H]istory file stating script is started (Code 2)
                6) Write HostName - Script name and version - O/S Name and version to the Log file (st.log_file)

        ----------
        st.stop()
        Example : st.stop(st.exit_code)   # Close SADM Environment
                sys.exit(st.exit_code)  # Exit To O/S
        ----------
            Accept one parameter - Either 0 (Successful) or non-zero (Error Encountered)
            Please call this function just before your script end.
            What this function do.
                1) If Exit Code is not zero, change it to 1.
                2) Get Actual Time and Calculate the Execution Time.
                3) Writing the Script Footer in the Log (Script Return code, Execution Time, ...)
                4) Update the RCH File (Start/End/Elapse Time and the Result Code)
                5) Trim The RCH File Based on User choice in sadmin.cfg
                6) Trim the Log based on user selection in sadmin.cfg
                7) Delete the PID File of the script (st.pid_file)
                8) Delete the User 3 TMP Files (st.tmp_file1, st.tmp_file2, st.tmp_file3)
        


    All variables content of the SADMIN configuration file are also accessible in your script.


        ====================================================================================================
        sadmlib_std_demo.py v3.6 - Library v3.02
        SADMIN CONFIG FILE VARIABLES           Description                           This System Result             
        ====================================================================================================
        [001] st.cfg_server                    SADMIN SERVER NAME (FQDN)           : holmes.maison.ca 
        [002] st.cfg_host_type                 SADMIN [C]lient or [S]erver         : S 
        [003] st.cfg_mail_addr                 SADMIN Administrator Default Email  : duplessis.jacques@gmail.com 
        [004] st.cfg_alert_type                0=NoMail 1=OnError 3=OnSuccess 4=All: 1 
        [005] st.cfg_alert_group               Default Alert Group                 : default 
        [006] st.cfg_alert_repeat              Seconds to wait before repeat alert : 21600 
        [007] st.cfg_textbelt_key              TextBelt.com API Key                :  
        [008] st.cfg_textbelt_url              TextBelt.com API URL                : https://textbelt.com/text 
        [009] st.cfg_cie_name                  Your Company Name                   : Your Cie Name 
        [010] st.cfg_domain                    Server Creation Default Domain      : maison.ca 
        [011] st.cfg_user                      SADMIN User Name                    : sadmin 
        [012] st.cfg_group                     SADMIN Group Name                   : sadmin 
        [013] st.cfg_www_user                  User that Run Apache Web Server     : apache 
        [014] st.cfg_www_group                 Group that Run Apache Web Server    : apache 
        [015] st.cfg_dbname                    SADMIN Database Name                : sadmin 
        [016] st.cfg_dbhost                    SADMIN Database Host                : sadmin.maison.ca 
        [017] st.cfg_dbport                    SADMIN Database Host TCP Port       : 3306 
        [018] st.cfg_rw_dbuser                 SADMIN Database Read/Write User     : sadmin 
        [019] st.cfg_rw_dbpwd                  SADMIN Database Read/Write User Pwd :  
        [020] st.cfg_ro_dbuser                 SADMIN Database Read Only User      : squery 
        [021] st.cfg_ro_dbpwd                  SADMIN Database Read Only User Pwd  :  
        [022] st.cfg_rrdtool                   RRDTOOL Binary Location             : /bin/rrdtool 
        [023] st.cfg_ssh_port                  SSH Port to communicate with client : 32 
        [024] st.cfg_nmon_keepdays             Nb. of days to keep nmon perf. file : 40 
        [025] st.cfg_rch_keepdays              Nb. days to keep unmodified rch file: 60 
        [026] st.cfg_log_keepdays              Nb. days to keep unmodified log file: 60 
        [027] st.cfg_max_rchline               Trim rch file to this max. of lines : 75 
        [028] st.cfg_max_logline               Trim log to this maximum of lines   : 500 
        [029] st.cfg_network1                  Network/Netmask 1 inv. IP/Name/Mac  : 192.168.1.0/24 
        [030] st.cfg_network2                  Network/Netmask 2 inv. IP/Name/Mac  :  
        [031] st.cfg_network3                  Network/Netmask 3 inv. IP/Name/Mac  :  
        [032] st.cfg_network4                  Network/Netmask 4 inv. IP/Name/Mac  :  
        [033] st.cfg_network5                  Network/Netmask 5 inv. IP/Name/Mac  :  
        [034] st.cfg_mksysb_nfs_server         AIX MKSYSB NFS Server IP or Name    : batnfs.maison.ca 
        [035] st.cfg_mksysb_nfs_mount_point    AIX MKSYSB NFS Mount Point          : /volume1/mksysb 
        [036] st.cfg_mksysb_backup_to_keep     AIX MKSYSB NFS Backup - Nb .to keep : 2 
        [037] st.cfg_rear_nfs_server           Rear NFS Server IP or Name          : batnas.maison.ca 
        [038] st.cfg_rear_nfs_mount_point      Rear NFS Mount Point                : /volume1/Linux_DR 
        [039] st.cfg_rear_backup_to_keep       Rear NFS Backup - Nb. to keep       : 3 
        [040] st.cfg_backup_nfs_server         NFS Backup IP or Server Name        : batnas.maison.ca 
        [041] st.cfg_backup_nfs_mount_point    NFS Backup Mount Point              : /volume1/backup_linux 
        [042] st.cfg_daily_backup_to_keep      Daily Backup to Keep                : 4 
        [043] st.cfg_weekly_backup_to_keep     Weekly Backup to Keep               : 4 
        [044] st.cfg_monthly_backup_to_keep    Monthly Backup to Keep              : 4 
        [045] st.cfg_yearly_backup_to_keep     Yearly Backup to keep               : 2 
        [046] st.cfg_weekly_backup_day         Weekly Backup Day (1=Mon,7=Sun)     : 5 
        [047] st.cfg_monthly_backup_date       Monthly Backup Date (1-28)          : 1 
        [048] st.cfg_yearly_backup_month       Yearly Backup Month (1-12)          : 12 
        [049] st.cfg_yearly_backup_date        Yearly Backup Date (1-31)           : 31 
        


    There is also a set a variables that you can use in your script to access SADMIN Directories.


        ====================================================================================================
        sadmlib_std_demo.py v3.6 - Library v3.02
        Client Directories Var. Avail.         Description                           This System Result             
        ====================================================================================================
        [001] st.base_dir                      SADMIN Root Directory               : /sadmin 
        [002] st.bin_dir                       SADMIN Scripts Directory            : /sadmin/bin 
        [003] st.tmp_dir                       SADMIN Temporary file(s) Directory  : /sadmin/tmp 
        [004] st.lib_dir                       SADMIN Shell & Python Library Dir.  : /sadmin/lib 
        [005] st.log_dir                       SADMIN Script Log Directory         : /sadmin/log 
        [006] st.cfg_dir                       SADMIN Configuration Directory      : /sadmin/cfg 
        [007] st.sys_dir                       Server Startup/Shutdown Script Dir. : /sadmin/sys 
        [008] st.doc_dir                       SADMIN Documentation Directory      : /sadmin/doc 
        [009] st.pkg_dir                       SADMIN Packages Directory           : /sadmin/pkg 
        [010] st.dat_dir                       Server Data Directory               : /sadmin/dat 
        [011] st.nmon_dir                      Server NMON - Data Collected Dir.   : /sadmin/dat/nmon 
        [012] st.dr_dir                        Server Disaster Recovery Info Dir.  : /sadmin/dat/dr 
        [013] st.rch_dir                       Server Return Code History Dir.     : /sadmin/dat/rch 
        [014] st.net_dir                       Server Network Information Dir.     : /sadmin/dat/net 
        [015] st.rpt_dir                       SYStem MONitor Report Directory     : /sadmin/dat/rpt 
        [016] st.dbb_dir                       Database Backup Directory           : /sadmin/dat/dbb 
        [017] st.setup_dir                     SADMIN Setup Directory.             : /sadmin/setup 
        [018] st.usr_dir                       User/System specific directory      : /sadmin/usr 
        [019] st.ubin_dir                      User/System specific bin/script Dir.: /sadmin/usr/bin 
        [020] st.ulib_dir                      User/System specific library Dir.   : /sadmin/usr/lib 
        [021] st.udoc_dir                      User/System specific documentation  : /sadmin/usr/doc 
        [022] st.umon_dir                      User/System specific SysMon Scripts : /sadmin/usr/mon 


        ====================================================================================================
        sadmlib_std_demo.py v3.6 - Library v3.02
        Server Directories Var. Avail.         Description                           This System Result             
        ====================================================================================================
        [001] st.www_dir                       SADMIN Web Site Root Directory      : /sadmin/www 
        [002] st.www_doc_dir                   SADMIN Web Site Root Directory      : /sadmin/www/doc 
        [003] st.www_dat_dir                   SADMIN Web Site Systems Data Dir.   : /sadmin/www/dat 
        [004] st.www_lib_dir                   SADMIN Web Site PHP Library Dir.    : /sadmin/www/lib 
        [005] st.www_tmp_dir                   SADMIN Web Temp Working Directory   : /sadmin/www/tmp 
        [006] st.www_perf_dir                  Web Performance Server Graph Dir.   : /sadmin/www/tmp/perf 
        


    There is also a set a variables that you can use in your script to access SADMIN Files.


        ====================================================================================================
        sadmlib_std_demo.py v3.6 - Library v3.02
        SADMIN FILES VARIABLES AVAIL.          Description                           This System Result             
        ====================================================================================================
        [001] st.pid_file                      Current script PID file             : /sadmin/tmp/sadmlib_std_demo.pid 
        [002] st.cfg_file                      SADMIN Configuration File           : /sadmin/cfg/sadmin.cfg 
        [003] st.cfg_hidden                    SADMIN Initial Configuration File   : /sadmin/cfg/.sadmin.cfg 
        [004] st.alert_file                    Alert Group Definition File Name    : /sadmin/cfg/alert_group.cfg 
        [005] st.alert_init                    Alert Group Initial File (Template) : /sadmin/cfg/.alert_group.cfg 
        [006] st.slack_file                    Alert - Slack Channel File          : /sadmin/cfg/alert_slack.cfg 
        [007] st.slack_init                    Alert - Slack Channel (Template)    : /sadmin/cfg/.alert_slack.cfg 
        [008] st.alert_hist                    Alert - History File                : /sadmin/cfg/alert_history.cfg 
        [009] st.alert_hini                    Alert - History Initial File        : /sadmin/cfg/.alert_history.cfg 
        [010] st.alert_seq                     Alert - Reference Counter           : /sadmin/cfg/alert_history.seq 
        [011] st.tmp_file1                     User usable Temp Work File 1        : /sadmin/tmp/sadmlib_std_demo_1.3843 
        [012] st.tmp_file2                     User usable Temp Work File 2        : /sadmin/tmp/sadmlib_std_demo_2.3843 
        [013] st.tmp_file3                     User usable Temp Work File 3        : /sadmin/tmp/sadmlib_std_demo_3.3843 
        [014] st.log_file                      Script Log File                     : /sadmin/log/holmes_sadmlib_std_demo.log 
        [015] st.rch_file                      Script Return Code History File     : /sadmin/dat/rch/holmes_sadmlib_std_demo.rch 
        [016] st.dbpass_file                   SADMIN Database User Password File  : /sadmin/cfg/.dbpass 
        [017] st.rpt_file                      SYStem MONitor report file          : /sadmin/dat/rpt/holmes.rpt 
        [018] st.backup_list                   Backup List File Name               : /sadmin/cfg/backup_list.txt 
        [019] st.backup_list_init              Initial Backup List (Template)      : /sadmin/cfg/.backup_list.txt 
        [020] st.backup_exclude                Backup Exclude List File Name       : /sadmin/cfg/backup_exclude.txt 
        [021] st.backup_exclude_init           Initial Backup Exclude (Template)   : /sadmin/cfg/.backup_exclude.txt 
        


    All these variables are filled automatically when you call the 'sadm_start' function.


        ====================================================================================================
        sadmlib_std_demo.py v3.6 - Library v3.02
        COMMAND PATH USE BY SADMIN STD. LIBR.  Description                           This System Result             
        ====================================================================================================
        [001] st.lsb_release                   Cmd. 'lsb_release', Get O/S Version : /bin/lsb_release 
        [002] st.dmidecode                     Cmd. 'dmidecode', Get model & type  : /sbin/dmidecode 
        [003] st.facter                        Cmd. 'facter', Get System Info      : /bin/facter 
        [004] st.bc                            Cmd. 'bc', Do some Math.            : /bin/bc 
        [005] st.fdisk                         Cmd. 'fdisk', Get Partition Info    : /sbin/fdisk 
        [006] st.which                         Cmd. 'which', Get Command location  : /bin/which 
        [007] st.perl                          Cmd. 'perl', epoch time Calc.       : /bin/perl 
        [008] st.mail                          Cmd. 'mail', Send SysAdmin Email    : /bin/mail 
        [009] st.mutt                          Cmd. 'mutt', Used to Send Email     : /bin/mutt 
        [010] st.curl                          Cmd. 'curl', To send alert to Slack : /bin/curl 
        [011] st.lscpu                         Cmd. 'lscpu', Socket & thread info  : /bin/lscpu 
        [012] st.nmon                          Cmd. 'nmon', Collect Perf Statistic : /bin/nmon 
        [013] st.parted                        Cmd. 'parted', Get Disk Real Size   : /sbin/parted 
        [014] st.ethtool                       Cmd. 'ethtool', Get System IP Info  : /sbin/ethtool 
        [015] st.ssh                           Cmd. 'ssh', SSH to SADMIN client    : /bin/ssh 
        [016] st.ssh_cmd                       Cmd. 'ssh', SSH to Connect to client: /bin/ssh -qnp 32                
        

    If variable content is blank, it means that the command is not available on the current system.
    At the end we have a Database connection test.


        ====================================================================================================
        sadmlib_std_demo.py v3.6 - Library v3.02
        Database Information                   Description                           This System Result             
        ====================================================================================================
        [001] st.dbsilent                      When DBerror, No ErrMsg (Just ErrNo): False 
        [002] st.usedb                         Script need (Open/Close) Database ? : True 
        Database connection succeeded
        Closing Database connection
        


 
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
 
SEE ALSO
sadm_template.sh    - Using the SADMIN Shell Template (sadm_template.sh)
sadm_template.py    - Using the SADMIN Python Template (sadm_template.py)
sadm_template_menu.sh    - Using the SADMIN Shell Menu Building Template (sadm_template_menu.sh)
sadm_wrapper.sh    - Use this wrapper to call your existing scripts and benefit of SADMIN tools.
sadmlib_std_demo.sh    - Show all global variables and functions you can use within your shell script, with examples.
sadmlib_std_demo.py    - Show all global variables and functions/modules you can use within your Python script, with examples. 