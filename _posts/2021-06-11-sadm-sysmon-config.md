---
title:          ${HOSTNAME}.smon
desc:           System Monitor configuration file. 
version:        3.0
summary: |         
    Ths is the SADMIN System Monitor (SysMon) configuration file. It MUST reside in "$SADMIN/cfg" 
    directory and MUST be named `hostname.smon`. Don't worry SADMIN setup script have all done that 
    for you. Blank line and line that start with a "#" (comment) are ignored. Each lines in the 
    SysMon configuration file is read and process one by one. After evaluating a line, the result 
    is recorded in column 2.
    {: .text-justify}
updated:        2021-06-11
os:             Linux, Aix, MacOS
type:           D  # [D]oc [S]=Server only [C]=Client [B]oth
categories:     [ system_monitor ] 
tags:           [ system_monitor ] 
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
$SADMIN/cfg/${HOSTNAME}.smon
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

Before the System Monitor exit, it write what we call a report file, which contain any error or 
warning detected while processing each line. This SysMon report file is named "hostname.rpt" and it
is created in the "$SADMIN/dat/rpt" directory. This file will then get transferred to the SADMIN 
server by the [sadm_fetch_client.sh]({% post_url 2021-03-16-sadm-fetch-client %}) for analysis and 
trigger an alert if needed.
{: .text-justify}
 

```bash
# include script
```

[Back to the top](#top_of_page)



<a id="examples"></a>
## EXAMPLE

```bash
root@holmes:/sadmin/cfg # cat holmes.smon
#----------------------------------------------------------------------------------------
# SADMIN SYStem MONitor configuration file (3.0)
#  - The file MUST reside in ${SADMIN}/cfg (filename `hostname`.smon).
#  - It is read when the SADMIN System Monitor start (sadm_sysmon.pl).
#  - Before exiting SysMon write the updated version of this file.
#  - Updated value (or resulting status) is recorded in the second column of each line
#  - New Filesystem are added automatically to this file when detected.
#  - Sysmon is run every 5 minutes from the sadm_server crontab (/etc/cron.d/sadm_server)
#  - Comments lines must always begin with a "#" (Column 1)
#  - Column are delimited by space(s) and/or tabulation.
#  - At execution each line is evaluated based on the test requested in the first column
#----------------------------------------------------------------------------------------
# Col   Name            Description
#----------------------------------------------------------------------------------------
#  1    IDENTIFIER      This name specify the test we want to run.
#                       These are the one presently supported :
#
#       'script:yourscript.sh'  
#               If you wish to run a custom script to you wrote, this is the one. 
#               Place the word 'script:' in column 1, followed by the name of your script. 
#               Be sure that your script exit with a return code of 0 or 1, so you can test it. 
#               Script execution time must be as short as possible, cause it will run each time 
#               the System Monitor is run.
#       load_average
#               Return system load average of the past 5 minutes, using 'uptime' (Linux,Aix,MacOS).
#               Actual value is returned in column 2 of the line.
#       cpu_level
#               Return cpu usage using 'vmstat' command (Linux/Aix) and 'iostat' on MacOS. 
#               The 'usr'added to the 'sys' value is returned in column 2 of the line.
#       swap_space
#               Return the percentage of the Swap/Paging Space used.
#               On Linux we use 'free | grep -i swap', on Aix 'lsps -a' and on MacOS 
#               'sysctl vm.swapusage'. Actual value is returned in column 2 of the line.
#       service_                
#               Return 1 if the service is active and 0 if it's not.
#               Service name follow the identifier prefix 'service_'.
#
#               They can be one or multiple service name specified.
#               Example, Redhat use 'crond' service name, Ubuntu use 'cron'. 
#               To test if the cron daemon is running on both system you specify multiple services.
#               Example : service_crond,cron
#               When specifying multiple service name, separate them by a comma ','. 
#               If one of them is active then 1 is returned.
#
#               If service is down, you can run one of your script to bring it up or used the 
#               one that come with SADMIN ($SADMIN/usr/mon/srestart.sh).
#               You can then put the restart script in the last field of the line, to get executed.
#               The script name you put in the last field must exist in '$SADMIN/usr/mon' directory 
#               and be executable. 
#               If the service is down the script will be executed, but no more than twice in a 
#               24 Hrs period. 
#               SADMIN SysMon does this by looking at column 6 (RunCounter), H (date) & I (Time).
#                   - The H and the I fields contain the date and time of the last script execution.
#                   - The Column 6 contain the number of time the script ran in the last 24 hrs.
#
#               With this information SysMon can now know if it was run in the last 24 hours. 
#                   - If it wasn't run in the last 24 Hrs, then the RunCounter(Col 6) is reset to 1,
#                     and the script specified at the end of the line is executed. 
#                   - If the script was executed in the last 24Hrs and if the RunCounter is less 
#                     than 2, then the script is executed. 
#                   - If the script was executed in the last 24Hrs and if the RunCounter is greater 
#                     than 1, the script is not executed, since it already ran twice in the last 
#                     24 hours.
#
#       daemon_ 
#               The function search to the specify "name" is present in the process list (ps) of 
#               the system. The search is case sensitive.
#               Example: "daemon_batcode"   
#                   - Will return 0 if 'batcode' is not in the process list.
#                   - Will return a value greater than zero, if it appear in the process list.
#                     If it appear four times, it will return 4.
#
#       check_multipath
#               SysMon check each path of the multipath and if one one them is not active or ready,
#               A value of 1 is returned if everything is ok or 0 when an error is detected. 
#               Line will only be evaluated if the command 'multipathd' is present on system.
#                       
#       http_   
#               Test the web site respond (1=Up 0=NoResponse)
#               Example : http_sysinfo.maison.ca
#
#       ping_
#               Every time Sysmon is run is will ping the name or the IP your have specified after 
#               the prefix 'ping_'.
#               Example : ping_www.google.com
#               This will ping the 'www.google.com' web site and return a 0 is it ping, if not a 1.
#
#       FS      Every time Sysmon is run the server smon configuration file is loaded in memory,
#               updated in memory during execution and then unloaded to disk when terminated.
#               So SysMon is able to know when a new filesystem is created on the system and it is
#               added automatically to his configuration file. 
#               The warning threshold is set to 80% and the error to 90%.
#               These are initial value, you can change them and they will remain to your setting.
#
#---------------------------------------------------------------------------------------------------
# Col   Name            Description
#  2    VALUE RETURNED  It's the value returned that is in conjunction with what is asked in col 1.
#                       For 'FS' it is the percentage used, for 'ping_' it will be a 0 or a 1, 
#                       for 'service_' it return 1 if the service is active and 0 if it's not.
#---------------------------------------------------------------------------------------------------
#  3    Operator        This dictate what operator will be used to compare the actual value (Col 2)
#       =,!=,<,>,=>,=<  with the 'Warning' (Col 4) and the 'Error' (Col 5).
#---------------------------------------------------------------------------------------------------
#  4    Warning Level   This value is compare against the value returned using the operator in 
#                       column 3. If it's True then a Warning is raise
#                       When you leave this value at 0, then the Warning threshold is not evaluated.
#---------------------------------------------------------------------------------------------------
#  5    Error Level     This value is compare against the value returned using the operator in 
#                       column 3. If it's True then an error is raise.
#                       When you leave this value at 0, then the Error threshold is not evaluated.
#---------------------------------------------------------------------------------------------------
#  6    Duration Min/   This field have a double usage :
#       RunCounter          - For load_average, cpu_level and swap_space it's the number of minutes
#                             that the value returned must exceed the Warning or Error before a 
#                             Warning or an Error is raised.
#                             Example : You set the warning threshold of the 'cpu_level' line at 80%
#                                       but you don't want to trigger an error if the CPU Level 
#                                       exceed 80% for only 2 minutes. So you may want to set this
#                                       column to 120 so an error would be trigger only when the cpu
#                                       level exceed 80% for at least 120 continuous minutes. If you
#                                       leave it 0, is sysmon is run at the cpu_level exceed 80% an
#                                       error will be trigger immediately.
#                           - For Service (service_) and Filesystem (FS) lines it represented the
#                             number of time the service was restarted or the filesystem was
#                             increase in the last 24 Hours. You don't need to change this field,
#                             it's taken care of automatically (Unless you want to reset it to 0 and
#                             provoke a service restart or a filesystem increase within the 24 hrs).
#---------------------------------------------------------------------------------------------------
#  7    Monitor         Hour of the day you want to enable evaluation of the line (In 24:00 format)
#       Start Time      Let's say you only want to evaluate a line between 7am and 9pm, you would
#                       put 0700 in this column and 2100 in column 8 (Monitor End Time)..
#                       If you leave this column at 0000 the line is evaluated 24 hours a day, 
#                       unless specify otherwise in column 9 to G.
#---------------------------------------------------------------------------------------------------
#  8    Monitor         Hour of the day you want to disable evaluation of the line (In 24:00 format)
#       End Time        Let's say you only want to evaluate a line between 7am and 9pm, you would
#                       put 0700 in column 7 and 2100 in this column (Monitor End Time)..
#                       If you leave this column at 0000 the line is evaluated 24 hours a day, 
#                       unless specify otherwise in column 9 to G.
#---------------------------------------------------------------------------------------------------
#  9    Enable Sunday   If this value is set to 'Y', the line will be evaluated on Sunday (Default).
#                       If this column is set to 'N', the line will not be evaluated on Sunday.
#---------------------------------------------------------------------------------------------------
#  A    Enable Monday   If this value is set to 'Y', the line will be evaluated on Monday (Default).
#                       If this column is set to 'N', the line will not be evaluated on Monday.
#---------------------------------------------------------------------------------------------------
#  B    Enable Tuesday  If this value is set to 'Y', the line will be evaluated on Tuesday (Default).
#                       If this column is set to 'N', the line will not be evaluated on Tuesday.
#---------------------------------------------------------------------------------------------------
#  C    Enable Wed.     If this value is set to 'Y', line will be evaluated on Wednesday (Default).
#                       If this column is set to 'N', line will not be evaluated on Wednesday.
#---------------------------------------------------------------------------------------------------
#  D    Enable Thursday If this value is set to 'Y', the line will be evaluated on Thursday(Default).
#                       If this column is set to 'N', the line will not be evaluated on Thursday.
#---------------------------------------------------------------------------------------------------
#  E    Enable Friday   If this value is set to 'Y', the line will be evaluated on Friday (Default).
#                       If this column is set to 'N', the line will not be evaluated on Friday.
#---------------------------------------------------------------------------------------------------
#  F    Enable Saturday If this value is set to 'Y', the line will be evaluated on Saturday(Default).
#                       If this column is set to 'N', the line will not be evaluated on Saturday.
#---------------------------------------------------------------------------------------------------
#  G    Active/Inactive If this value is set to 'Y', the line will always be evaluated (Default)
#                       If this column is set to 'N', the line will never be evaluated.
#                       This is used, when you want temporarely deactivate a line.
#---------------------------------------------------------------------------------------------------
#  H    Last Event Date This column contain the date of the last event (script execution, cpu_level
#                       exceeded, swap_space exceeded, filesystem increase, service restarted,..)
#                       If it used by sysmon when condition are related to time period.
#                       You don't need to change this field, sysmon take care of it.
#---------------------------------------------------------------------------------------------------
#  I    Last Event Time This column contain the time of the last event (script execution, cpu_level
#                       exceeded, swap_space exceeded, filesystem increase, service restarted,..)
#                       If it used by sysmon when condition are related to time period.
#                       You don't need to change this field, sysmon take care of it.
#---------------------------------------------------------------------------------------------------
#  J    Warning Alert Group
#                       Alert Group to advise when a warning need to be issue.
#                       Group MUST be defined in the Alert Group File ($SADMIN/cfg/alert_group.cfg)
#                       When new filesystem line are added the default group used for Warning/Error
#                       is the one defined sadmin configuration file ($SADMIN/cfg/sadmin.cfg)
#---------------------------------------------------------------------------------------------------
#  K    Error Alert Group 
#                       Alert Group to advise when an error need to be issue.
#                       Group MUST be defined in the Alert Group File ($SADMIN/cfg/alert_group.cfg)
#                       When new filesystem line are added the default group used for Warning/Error
#                       is the one defined sadmin configuration file ($SADMIN/cfg/sadmin.cfg)
#---------------------------------------------------------------------------------------------------
#  L    Script Name     Never use by sysmon if the column is blank or contain '-'.
#                       When the line is evaluated and it turn out to be in error, if you put a
#                       script name it will be executed (You may want to correct the error with it).
#                       Script MUST reside in $SADMIN/usr/mon directory and be executable.
#                       The script will produce a log in that same directory, with the same name as 
#                       your script.
#                       File filesystem increase, the name of the script MUST be 'sadm_fs_incr.sh'.
#---------------------------------------------------------------------------------------------------
# IDENTIFIER - COLUMN 1          2  3   4   5   6  7    8   9 A B C D E F G     H     I   J    K   L
#---------------------------------------------------------------------------------------------------
#
# ----- Run specific scripts, check return code and issue a warning or error based on threshold
# Example 
#script:stemplate.sh       1  =  00  01 000 0000 0000 Y Y Y Y Y Y Y Y 20180911 1520 default default -
#
#
# ----- Aix/Linux/MacOS CPU Load, Server Load Average and Swap Space usage Monitoring
load_average                     0  >  20  35 120 0700 2100 Y Y Y Y Y Y Y Y 00000000 0000 default default -
cpu_level                        1 >=  85  95 240 0700 2100 Y Y Y Y Y Y Y Y 00000000 0000 default default -
swap_space                       3  >  85  90 000 0000 0000 Y Y Y Y Y Y Y Y 20180911 1520 default default -
#
# ----- Linux Common Service Monitoring
service_crond,cron               1  <  00  01 000 0000 0000 Y Y Y Y Y Y Y Y 20180820 1520 default default srestart.sh
service_chronyd                  1  <  00  01 000 0000 0000 Y Y Y Y Y Y Y Y 20180820 1520 default default srestart.sh
service_ssh,sshd                 1  <  00  01 000 0000 0000 Y Y Y Y Y Y Y Y 20180820 1520 default default srestart.sh
service_postfix                  1  <  00  01 000 0000 0000 Y Y Y Y Y Y Y Y 20180820 1520 default default srestart.sh
service_at,atd                   1  <  00  01 000 0000 0000 Y Y Y Y Y Y Y Y 20180820 1520 default default srestart.sh
#service_systemd-resolved         0  <  00  01 002 0000 0000 Y Y Y Y Y Y Y Y 20210606 1035 default default srestart.sh
#
#service_sendmail                 1  <  00  01 000 0000 0000 Y Y Y Y Y Y Y Y 20180820 1520 default default srestart.sh
#service_ntp,ntpd               0  <  00  01 000 0000 0000 Y Y Y Y Y Y Y Y 20180820 1520 default default srestart.sh
#service_syslog,rsyslog,syslogd   0  <  00  01 000 0000 0000 Y Y Y Y Y Y Y Y 20180820 1520 default default srestart.sh
#
# DNS Service
#service_named                    0  <  00  01 000 0000 0000 Y Y Y Y Y Y Y Y 20180820 1520 default default srestart.sh
#service_named-chroot             0  <  00  01 000 0000 0000 Y Y Y Y Y Y Y Y 20180820 1520 default default srestart.sh
#
# DHCP Service
#service_dhcpd                    0  <  00  01 000 0000 0000 Y Y Y Y Y Y Y Y 20180820 1520 default default srestart.sh
#
# ----- Monitor Daemon or Process Running 
#daemon_mydaemon                 1  <  00  01 000 0000 0000 Y Y Y Y Y Y Y Y 20180820 1520 default default -
#
# ----- Check Linux Multipath Status (0=Error 1=All path(s) are Online/Ready)
check_multipath                  1 !=  00  01 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 default default -
#
# Ping server (Return 0=Ok 1=Error) Line below raise a Warning if site doesn't respond to ping.
#ping_www.google.com              0  =  01  00 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 default default -

# Ping server (Return 0=Ok 1=Error) Line below raise an Error if site doesn't respond to ping.
#ping_www.ibm.com                 0  =  00  01 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 default default -
#
#
#
# ----- Filesystem Monitoring
# Can increase it by 10%, two times within 24hours maximum, if script "sadm_fs_incr.sh" in Column L.
# FS/example                    23 >=  25  90 001 0000 0000 Y Y Y Y Y Y Y Y 20180615 0824 default default sadm_fs_incr.sh
#---------------------------------------------------------------------------------------------------
# IDENTIFIER - COLUMN 1          2  3   4   5   6  7    8   9 A B C D E F G     H     I   J    K   L
#---------------------------------------------------------------------------------------------------
#
#SADMSTAT 2.5 holmes - Sat Feb  4 09:56:10 2017 - Execution Time 5.00 seconds
FS/           39 >=  85  90 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 default default -
FS/usr        72 >=  85  90 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 default default -
FS/boot       53 >=  85  90 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 default default -
FS/wiki        5 >=  85  90 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 default default -
FS/wsadmin    82 >=  80  90 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 default default -
FS/backups    64 >=  85  90 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 default default -
FS/psadmin     4 >=  85  90 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 default default -
FS/storix     12 >=  85  90 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 default default -
FS/opt        71 >=  85  90 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 default default -
FS/tmp         1 >=  85  90 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 default default -
FS/sysadmin    9 >=  85  90 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 default default -
FS/linternux   4 >=  85  90 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 default default -
FS/var        27 >=  85  90 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 default default -
FS/sadmin     38 >=  85  90 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 default default -
FS/home       55 >=  85  90 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 default default -
FS/install     6 >=  85  90 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 default default -
FS/gitrepos   10 >=  85  90 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 default default -
FS/history     1 >=  85  90 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 default default -
#SYSMON 2.43 holmes - Last Boot: 2021-05-28 07:16:27 - Mon Jun 14 11:07:04 2021 - Execution Time 2.00 seconds
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
| [sadm_sysmon_tui.pl]({% post_url 2021-05-18-sadm-sysmon-tui %})                   |  Command line summary of alerts and failed scripts of all your servers.  
| [sadm_sysmon.pl]({% post_url 2021-06-10-sadm-sysmon %})                           | Client system monitor   
| [sadm_fetch_client.sh]({% post_url 2021-03-16-sadm-fetch-client %})               | rsync all .rch/.log/.rpt from actives clients to the SADMIN server  
| [SysMon configuration file]({% post_url 2021-06-11-sadm-sysmon-config %})         | Client System Monitor configuration file   
| [sadmin.cfg]({% post_url 2021-04-26-sadmin-cfg %})                                | SADMIN main configuration file   

