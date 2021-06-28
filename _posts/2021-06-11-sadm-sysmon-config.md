---
title:          SysMon configuration file 'hostname'.smon
desc:           System Monitor configuration file. 
version:        3.0
summary: |         
    This is the SADMIN System Monitor (SysMon) configuration file. It MUST reside in "$SADMIN/cfg" 
    directory and MUST be named `hostname.smon`. Don't worry SADMIN setup script have all done that 
    for you. Blank line and line that start with a "#" (comment) are ignored. 
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
toc:            true
classes:        wide
sidebar:
  title:        "Documentation"
  nav:          sidebar-manpage
---
<a id="top_of_page"></a>

{% include sadm/sadm_page_info.md %}
{% if page.type == "S" %}
<font size="3"><strong>Can only be run on SADMIN Server.</strong></font>
{% endif %}
{% if page.type == "B" %}
<font size="3"><strong>Can be executed on a client and on the SADMIN Server.</strong></font>
{% endif %}
<br>
{{ page.summary }} 

### General background of Sysmon configuration file

- The file MUST reside in ${SADMIN}/cfg (filename `hostname`.smon).
- It is read when the SADMIN System Monitor start (sadm_sysmon.pl).
- New Filesystem are added automatically to this file.
- Sysmon is run every 5 minutes from the sadm_server crontab (/etc/cron.d/sadm_server)
- Each lines in the SysMon configuration file is evaluated and process one by one. 
- After evaluating a line, the result is recorded in column 2.
- Before exiting SysMon write the updated version of the file.
- Each time the system monitor run, the last line of the configuration file is updated. We can see 
the System Monitor version number, the server name, the last boot date, the current date and finally 
the time it took to process all the requested tests. 
```perl
#SYSMON 2.43 holmes, Boot 2021-05-28 07:16:27, Sat Jun 12 10:47:03 2021, Run 1.00 sec
``` 
- Before the System Monitor exit, it write what we call a report file, which contain any error or 
warning detected while processing each line. This SysMon report file is named "hostname.rpt" and it
is created in the "$SADMIN/dat/rpt" directory. This file will then get transferred to the SADMIN 
server by the [sadm_fetch_client.sh]({% post_url 2021-03-16-sadm-fetch-client %}) for analysis and 
trigger an alert if needed.
{: .text-justify}

### Format of the file

- Comments lines must always begin with a "#" (Column 1)
- Column are delimited by space(s) and/or tabulation.
- Updated value (or resulting status) is recorded in the second column of each line
- At execution each line is evaluated based on the test requested in the first column
- Column 1 dictate the kind of test that will performed on that line.

![Sysmon configuration file format example](/assets/img/sadm_sysmon/sadm_sysmon_config_ref.png){: .align-center}




### Conditions for a line to be evaluated

Before a line is evaluated it must meet certain conditions specified by certain column on that same
line. All the conditions below must be met before a line is evaluated.

- **Line Active or Inactive (Column G)**    
When this column is set to 'Y' (Active), then the line met the first condition to get evaluated 
(Default). If set to 'N' (Inactive), the line is not evaluated and SysMon continue with the next 
line in SysMon config file. This column can be use to temporarily deactivate a line.
{: .text-justify}

- **Monitor Start Time (Column 7) and End Time (Column 8)**    
These two columns represent the start time and end time for a line to be evaluated. If one of these 
two columns is zero then the line met the second condition to get evaluated. The start time 
column (7) represent the hour of the day you want to start evaluation of the line (In 24:00 format),
the end time in column (8), is the hour of the day you want to disable evaluation of the line. For 
example, let's say you only want to evaluate a line only between 7am and 9pm, you would put '0700' 
(Monitor Start Time) in column 7 and '2100' in column 8 (Monitor End Time).
{: .text-justify}


- **Particular day to evaluate (Column 9 to F)**   
Each of these columns represent a day of the week. Column 9 represent Sunday, 'A' Monday, 
'B' Tuesday, 'C' Wednesday, 'D' Thursday, 'E' Friday and finally 'F' Saturday. By default, all of 
these columns contain a 'Y' meaning that he line is evaluated every day of the week. If you want to
disable line evaluation on Saturday and Sunday, you would put 'N' in column '9' and 'F'.
{: .text-justify}


- **Last event date (Col H) & time (Col I) vs Minimum duration/Run Counter (Col 6)**   
When Sysmon monitor the CPU usage level for example, you don't want to be alerted every time the 
CPU reach the warning or error level. This is where column 6 come in handy, you specify in column 6
the continuous number of minutes the CPU must exceed the warning or error level, before being 
alerted. For example if you put '060' in column 6 then the alert would be generated only when the 
CPU usage exceed the warning or error level for more than 60 minutes. To be able to do that, Sysmon
need know when was the date and time of the first alert, this is recorded in column 'H' and 'I'.
Every time the CPU level is under the warning and error level, column 'H' and 'I' are set back to
zero. The same logic apply to 'Load average' and the 'Swap Space'.    
For Service (service_) and Filesystem (FS) lines, column 6 it represented the number of time the 
service was restarted or the filesystem increased was attempted in the last 24 Hours. You don't 
need to change this field, it's taken care of automatically (Unless you want to reset it to 0 and 
provoke a service restart or a filesystem increase within the 24 hrs). Every time a service is 
restarted column 6 is increase by one. Service can't be restarted more than 2 times every 24 hours,
same thing for the filesystem increase, only two filesystems increase per 24 hours can be done 
(each 10% increase). Again when the service is restarted, or fileystem get lower than warning 
and error level then col 6, column 'H' and 'I get reset to 0. To be able to do that, Sysmon
need know when was the date and time of the first alert, this is recorded in column 'H' and 'I'.
{: .text-justify}

[Back to the top](#top_of_page)



### Warning alert group
Column 'J' represent the Warning Alert Group to advise when a warning need to be issue. Group MUST 
be defined in the Alert Group File ($SADMIN/cfg/alert_group.cfg). When new filesystem line are 
added the default group used for Warning/Error is the one defined sadmin configuration file 
($SADMIN/cfg/sadmin.cfg).
{: .text-justify}

[Back to the top](#top_of_page)



### Error alert group
Column 'K' represent the Error Alert Group to advise when a error need to be issue. Group MUST 
be defined in the Alert Group File ($SADMIN/cfg/alert_group.cfg). When new filesystem line are 
added the default group used for Warning/Error is the one defined sadmin configuration file 
($SADMIN/cfg/sadmin.cfg).
{: .text-justify}

[Back to the top](#top_of_page)





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


#       swap_space
#               Return the percentage of the Swap/Paging Space used.
#               On Linux we use 'free | grep -i swap', on Aix 'lsps -a' and on MacOS 
#               'sysctl vm.swapusage'. Actual value is returned in column 2 of the line.
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


#---------------------------------------------------------------------------------------------------
# IDENTIFIER - COLUMN 1          2  3   4   5   6  7    8   9 A B C D E F G     H     I   J    K   L
#---------------------------------------------------------------------------------------------------
```



<a id="runningscript"></a>
### Running you own script

L    Script Name   
Never use by sysmon if the column is blank or contain '-'.
When the line is evaluated and it turn out to be in error, if you put a
script name it will be executed (You may want to correct the error with it).
Script MUST reside in $SADMIN/usr/mon directory and be executable.
The script will produce a log in that same directory, with the same name as 
your script.
File filesystem increase, the name of the script MUST be 'sadm_fs_incr.sh'.

```bash
# ----- Run specific scripts, check return code and issue a warning or error based on threshold
# IDENTIFIER - COLUMN 1          2  3   4   5   6  7    8   9 A B C D E F G     H     I   J    K   L
#script:stemplate.sh       1  =  00  01 000 0000 0000 Y Y Y Y Y Y Y Y 20180911 1520 default default -
#
```
[Back to the top](#top_of_page)




<br>
<a id="loadaverage"></a>
### Load average

- Return system load average of the past 5 minutes, using 'uptime' (Linux,Aix,MacOS).  
- Actual value is returned in column 2 of the line.  
  
```bash
#
# ----- Aix/Linux/MacOS CPU Load, Server Load Average and Swap Space usage Monitoring
# IDENTIFIER - COLUMN 1          2  3   4   5   6  7    8   9 A B C D E F G     H     I   J    K   L
load_average                     0  >  20  35 120 0700 2100 Y Y Y Y Y Y Y Y 00000000 0000 default default -
```
[Back to the top](#top_of_page)




<br>
<a id="cpuusage"></a>
### Check CPU usage

- Return cpu usage using 'vmstat' command (Linux/Aix) and 'iostat' on MacOS. 
- The 'usr' added to the 'sys' value is returned in column 2 of the line.

```bash
# IDENTIFIER - COLUMN 1          2  3   4   5   6  7    8   9 A B C D E F G     H     I   J    K   L
cpu_level                        1 >=  85  95 240 0700 2100 Y Y Y Y Y Y Y Y 00000000 0000 default default -
```
[Back to the top](#top_of_page)



### Check Swap Space utilization

```bash
# IDENTIFIER - COLUMN 1          2  3   4   5   6  7    8   9 A B C D E F G     H     I   J    K   L
swap_space                       3  >  85  90 000 0000 0000 Y Y Y Y Y Y Y Y 20180911 1520 default default -
```
[Back to the top](#top_of_page)




### Service Monitoring
                
- Return 1 if the service is active and 0 if it's not.
- Service name follow the identifier prefix 'service_'.
- They can be one or multiple service name specified.
- Example, Redhat use 'crond' service name, Ubuntu use 'cron'. 
- To test if the cron daemon is running on both system you specify multiple services.
- Example : service_crond,cron
- When specifying multiple service name, separate them by a comma ','. 
- If one of them is active then 1 is returned.
- If service is down, you can run one of your script to bring it up or used the 
- one that come with SADMIN ($SADMIN/usr/mon/srestart.sh).
- You can then put the restart script in the last field of the line, to get executed.
- The script name you put in the last field must exist in '$SADMIN/usr/mon' directory 
- and be executable. 
- If the service is down the script will be executed, but no more than twice in a 
- 24 Hrs period. 
- SADMIN SysMon does this by looking at column 6 (RunCounter), H (date) & I (Time).
-     - The H and the I fields contain the date and time of the last script execution.
-     - The Column 6 contain the number of time the script ran in the last 24 hrs.
- With this information SysMon can now know if it was run in the last 24 hours. 
-     - If it wasn't run in the last 24 Hrs, then the RunCounter(Col 6) is reset to 1,
-       and the script specified at the end of the line is executed. 
-     - If the script was executed in the last 24Hrs and if the RunCounter is less 
-       than 2, then the script is executed. 
-     - If the script was executed in the last 24Hrs and if the RunCounter is greater 
-       than 1, the script is not executed, since it already ran twice in the last 
-       24 hours.

```bash
#
# ----- Linux Common Service Monitoring
# IDENTIFIER - COLUMN 1          2  3   4   5   6  7    8   9 A B C D E F G     H     I   J    K   L
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
```

[Back to the top](#top_of_page)




### Daemon running

```bash
#
# ----- Monitor Daemon or Process Running 
# IDENTIFIER - COLUMN 1          2  3   4   5   6  7    8   9 A B C D E F G     H     I   J    K   L
#daemon_mydaemon                 1  <  00  01 000 0000 0000 Y Y Y Y Y Y Y Y 20180820 1520 default default -
```
[Back to the top](#top_of_page)



<a id="multipath"></a>
### Multipath test

Again if the minimum requirements are met then multipath state evaluation is done, if not we proceed 
with the next line of Sysmon configuration file.
SysMon check each path of the multipath and if one one them is not active or ready,
A value of 1 is returned if everything is ok or 0 when an error is detected. 
Line will only be evaluated if the command 'multipathd' is present on system.
    if ( $OSNAME eq "aix" )  {return ;}                                 # Multipath Oonly on Linux
    if ( $SYSMON_DEBUG >= 5) {print "\n\nChecking Multipath ...";}      # Show User what were doing
    if ( $CMD_MPATHD eq "" ) {                                          # If multipathd is not host
        print "Status of Multipath skipped - Command multipathd not present on system";
    }

    # Get output of multipathd and analyse it
    open(FPATH, "echo 'show paths' | $CMD_MPATHD -k 2>/dev/null| grep -vEi 'cciss|multipath' | ")
        or die "Can't execute $CMD_MPATHD \n";

    $SADM_RECORD->{SADM_CURVAL} = 1 ;                                   # Default Status is OK=1
    $INUSE = 0 ;                                                        # Multipath Not in Use=0
    while ($line = <FPATH>) {                                           # Read multipathd output
        @ligne = split ' ',$line;                                       # Split Line into Array
        ($mhcli,$mdev,$mmajor,$mdum1,$mstatus,$mdum2,$mdum3) = @ligne;  # Split Array in fields
        print "\nMultipath Status = $mstatus";                          # Show User current Status
        if ($mstatus ne "[active][ready]") {                            # Current Status != Active
            $SADM_RECORD->{SADM_CURVAL} = 0;                            # Current Status to Error=0
            print "Multipath Error Detected" ;                          # Signal that Error Detected
        }
        $INUSE = 1;                                                     # Multipath is in use Flag
    }
    close FPATH ;                                                       # Close multipathd output
    if ($INUSE == 0){ $mstatus = "not in use"; }                        # Set Status to 'not is use'

    # Set Parameter of Current Evaluation, ready to be evaluated.
    $CVAL = $SADM_RECORD->{SADM_CURVAL} ;                               # Current Value
    $WVAL = $SADM_RECORD->{SADM_WARVAL} ;                               # Warning Threshold Value
    $EVAL = $SADM_RECORD->{SADM_ERRVAL} ;                               # Error Threshold Value
    $TEST = $SADM_RECORD->{SADM_TEST}   ;                               # Test Operator (=,<=,!=,..)
    $MOD  = "linux"                     ;                               # Module Category
    $SMOD = "MUTIPATH"                  ;                               # Sub-Module Category
    $STAT = $mstatus                    ;                               # Current Status Returned
    if ($SYSMON_DEBUG >= 5) {                                           # Debug Level at least 5
        printf "\nMultipath status is %s - Code = (%d) (1=ok 0=Error)",$STAT,$CVAL; # Show User
    }
    check_for_error($CVAL,$WVAL,$EVAL,$TEST,$MOD,$SMOD,$STAT);          # Go Evaluate Error/Alert
}   
```bash
#
# ----- Check Linux Multipath Status (0=Error 1=All path(s) are Online/Ready)
# IDENTIFIER - COLUMN 1          2  3   4   5   6  7    8   9 A B C D E F G     H     I   J    K   L
check_multipath                  1 !=  00  01 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 default default -
```
[Back to the top](#top_of_page)



<a id="pingtest"></a>
### Ping test (Line that begin with 'ping_')

To execute a ping test, the column one must begin with 'ping_' follow by the tcp/ip address or 
the hostname you would like to ping. Example, to ping 'www.google.com' the column one would be 
"ping_www.google.com". This will ping the 'www.google.com' web site and return a 0 if it ping, 
if not a 1 and the result is always place in column 2. Worth mentioning that the ping tries three
times to ping (ping -c3) before indicating an error.
It the example below we can see that 'www.google.com' did respond to the ping (column 2 = 0) and
that 'www.ibm.com' did not respond to our ping (column 2 = 1). 
{: .text-justify}

```bash
# Ping server (Return 0=Ok 1=Error) 
# ID COLUMN 1       2  3  4  5  6    7   8   9 A B C D E F G     H      I     J        K        L
ping_www.google.com 0  = 01 00 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 default sms_sysadmin -
ping_www.ibm.com    1  = 00 01 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 default sms_sysadmin -
#
```

- If '**www.google.com**" didn't respond to the ping, we would get a ´1´ in column 2 and it would 
equal (column 3) to the '1' in column 4, this means that a warning alert would be issue to the
'default' alert group specify in column 'J'. If the Alert group file was define like below, with 
the 'default' group having a type 'm', then an email would be sent to the "mail_webteam" with 
contain two emails addresses "webteam@acme.com, sysadmin@acme.com", so these two addresses would 
receive an email alert.  
{: .text-justify}

- In '***www.ibm.com***' example below, we can see that the ping to 'www.ibm.com' didn't work 
(column 2 = 1) and we see that the 'Error' threshold is also set to '1' and the test to do between 
these two values is '='. So the result (column 2) is '1', the test (column 3) is '=', the 'warning'
threshold (column 4) is '0' (So we forget about it), and the 'Error' threshold (column 5) is '1', 
so this generate 'Error' alert. The 'Error' alert will be send to the alert group specify in column 
'K' witch is 'sms_sysadmin'. So a SMS Alert would be sent to the "sms_sysadmin" group which contain 
one member "cell_john_doe", so the SMS will go to the cellular number '5147577706'.
{: .text-justify}

```
default             m   mail_webteam
#
# Email Alert Group 
mail_sysadmin       m   sysadmin@acme.com
mail_webteam        m   webteam@acme.com,sysadmin@acme.com 
#
# SMS (Texto) Alert Group, members are Cellular name
sms_sysadmin        t   cell_john_doe  
#
# Cellular number of individual (Use only in SMS alert group)
cell_john_doe       c   5147577706

```

- We state before that column 4 is the 'Warning' value or threshold and that column 5 is the 'Error'
value or threshold. Whenever one of these value is zero, it means that there no threshold for that 
column and that it will not be evaluated.

[Back to the top](#top_of_page)




### Filesystem monitoring (Line beginning with 'FS')

SysMon automatically detect new filesystem on the system and add them to the [SysMon configuration file]({% post_url 2021-06-11-sadm-sysmon-config %}) and can check a filesystem usage and . By default,it will set 
the "Warning" usage level to 85% and the "Error" at 90%. If the file system usage is greater or 
equal to 85% and less than 90% it will shows up in the System Monitor web page as a "Warning". 
If the usage is equal or greater than 90%, it will appear an an "Error" is the System Monitor 
web page and an alert is generated. In the example below, I have change the warning threshold from 
85% to 80% in the fourth column to raise a warning.

Every time Sysmon is run the server smon configuration file is loaded in memory,
updated in memory during execution and then unloaded to disk when terminated.
So SysMon is able to know when a new filesystem is created on the system and it is
added automatically to his configuration file. 
The warning threshold is set to 80% and the error to 90%.
These are initial value, you can change them and they will remain to your setting.

```
# COLUMN 1    2  3   4   5   6  7    8   9 A B C D E F G     H     I      J        K   L
FS/wsadmin   82 >=  80  90 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 default default -
```
If a line in the [SysMon configuration file]({% post_url 2021-06-11-sadm-sysmon-config %}) begin
with "FS", this indicate that this line is used to test the filesystem usage. In the example above
we are evaluating the "/wsadmin" filesystem usage. It is currently using 82% and we've set the
warning level at 80% and the error level at 90%. Since we are above the warning level (and below the
error level), this have trigger an warning alert. 

![Sysmon Warning on Web](/assets/img/sadm_sysmon/sadm_sysmon_filesystem_warning.png){: .align-center} 

The warning will always appear on the system monitor web page, like the example below. 

![Sysmon Warning on Web](/assets/img/sadm_sysmon/sadm_sysmon_warning_email.png){: .align-center} 

```bash
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

[Back to the top](#top_of_page)


<a id="seealso"></a>
## See also

| Link to ...| Description |  
| :--- | :--- |  
| [sadm_sysmon_tui.pl]({% post_url 2021-05-18-sadm-sysmon-tui %})                   |  Command line summary of alerts and failed scripts of all your servers.  
| [sadm_sysmon.pl]({% post_url 2021-06-10-sadm-sysmon %})                           | Client system monitor   
| [sadm_fetch_client.sh]({% post_url 2021-03-16-sadm-fetch-client %})               | rsync all .rch/.log/.rpt from actives clients to the SADMIN server  
| [SysMon configuration file]({% post_url 2021-06-11-sadm-sysmon-config %})         | Client System Monitor configuration file   
| [sadmin.cfg]({% post_url 2021-04-26-sadmin-cfg %})                                | SADMIN main configuration file   

