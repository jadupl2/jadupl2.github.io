---
title:          SysMon configuration file 'hostname'.smon
desc:           System Monitor configuration file. 
version:        3.0
summary: |         
    This is the SADMIN System Monitor (SysMon) configuration file. It MUST reside in "$SADMIN/cfg" 
    directory and MUST be name "$(hostname -s).smon". Don't worry SADMIN setup script have all 
    done that for you. Blank line and line that start with a "#" (comment) are ignored. 
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


### General background of Sysmon configuration file

- The System Monitor (SysMon) configuration file MUST reside in "$SADMIN/cfg" directory and MUST be 
name "$(hostname -s).smon". Don't worry SADMIN setup script have all done that for you. Blank line 
and line that start with a "#" (comment) are ignored.  
- The configuration is loaded in memory when the [SADMIN System Monitor]({% post_url 2021-06-10-sadm-sysmon %}) start.
- If new filesystem are detected by SysMon they are added automatically to this file.  
- Sysmon is run every 5 minutes from the [sadm_server crontab]({% post_url 2021-06-25-etc-crond-sadm-server %}).
- Each lines in the SysMon configuration file is evaluated and process one by one. 
- After evaluating a line, the result is recorded in column 2.
- Before exiting SysMon write the updated version of the Sysmon configuration file.
- Each time the system monitor run, the last line of the configuration file is updated. We can see 
the System Monitor version number, the server name, the last boot date, the current date and finally 
the time it took to process all the requested tests. 
```perl
#SYSMON 2.43 holmes, Boot 2021-05-28 07:16:27, Sat Jun 12 10:47:03 2021, Run 1.00 sec
``` 
- Before the System Monitor exit, it write what we call a report file, which contain any error or 
warning detected while processing each line. This SysMon report file is named "$(hostname -s).rpt" 
and it's created in the "$SADMIN/dat/rpt" directory. This file will then get transferred to the SADMIN 
server by the [sadm_fetch_client.sh]({% post_url 2021-03-16-sadm-fetch-client %}) for analysis and 
trigger an alert if needed.
```bash
# cat $SADMIN/dat/rpt/holmes.rpt 
Warning;holmes;2021.06.29;10:47;linux;FILESYSTEM;Filesystem /wsadmin at 82% >= 80%;default;default
```
{: .text-justify}



### Format of the Sysmon configuration file

- Comments lines must always begin with a "#" (Column 1)
- Column are delimited by space(s) and/or tabulation.
- Updated value (or resulting status) is recorded in the second column of each line
- At execution each line is evaluated based on the test requested in the first column
- Column 1 dictate the kind of test that will performed on that line.

**Here is a diagram that explain each column of the Sysmon configuration file**

[![Sysmon configuration file format example](/assets/img/sadm_sysmon/sadm_sysmon_config_ref.png)](/assets/img/sadm_sysmon/sadm_sysmon_config_ref.png){: .align-center}



<a id="sysmon_conditions"></a>
### Conditions for a line to be evaluated

You may not want to perform a test every time the system monitor run. For example, you may not want
to test the CPU utilization on the weekend, because you know you will be running some batch job and
it will take more CPU and this is normal. Or just disable it on Saturday between 1am and 7am, this
is the kind of conditions we will take a look below.   
Before a line is evaluated it must meet certain conditions specified by certain column on that same
line. All the conditions below must be met before a line is evaluated.
{: .text-justify}

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
these columns contain a 'Y' meaning that the line is evaluated every day of the week. For example, 
if you want to disable line evaluation on Saturday and Sunday, you would put 'N' in column '9' and 'F'.
{: .text-justify}


- **Last event date (Col H) & time (Col I) vs Minimum duration/Run Counter (Col 6)**   
    - When Sysmon monitor the CPU usage level for example, you don't want to be alerted every time the 
CPU reach the warning or error level. For example, you want to be alerted, if the CPU utilization 
is above the 'Error' level for more than 30 minutes. This is when column 6 come in handy, you 
specify in column 6 the continuous number of minutes the CPU must exceed the warning or error 
level, before being alerted. For example if you put '060' in column 6 then the alert would be 
generated only when the CPU usage exceed the warning or error level for more than 60 minutes. 
To be able to do that, Sysmon need know when was the date and time of the first alert, this is 
recorded in column 'H' and 'I'. Every time the CPU level is under the warning and error level, 
column 'H' and 'I' are set back to zero. *The same logic apply to 'Load average' and the 'Swap Space'*.    

    - For Service (service_), custom script execution and filesystem (FS) lines, column 6 represent 
the number of time the service was restarted or the filesystem increased was attempted in the 
last 24 Hours. You don't need to change this field, it's taken care of automatically (Unless you 
want to reset it to 0 and provoke a service restart or a filesystem increase within the 24 hrs). 
Every time a service is restarted column 6 is increase by one. Service can't be restarted 
automatically more than 2 times every 24 hours, same thing for the filesystem increase, only two 
filesystems increase per 24 hours can be done (each 10% increase). Again when the service is 
restarted, or fileystem get lower than warning and error level then col 6, column 'H' and 'I get 
reset to 0. To be able to do that, Sysmon need know when was the date and time of the first alert, 
this is recorded in column 'H' and 'I'.
{: .text-justify}



```
service_cron,crond               1  <  00  01 000 0000 0000 Y Y Y Y Y Y Y Y 20180820 1520 default default srestart.sh
service_postfix                  1  <  00  01 000 0000 0000 Y Y Y Y Y Y Y Y 20180820 1520 default default
```
[Back to the top](#top_of_page)


<a id="sysmon_warning_group"></a>
### Warning alert group
Column 'J' represent the Warning Alert Group to advise when a warning need to be issue. Group MUST 
be defined in the Alert Group File ($SADMIN/cfg/alert_group.cfg). When new filesystem line are 
added the default group used for Warning/Error is the one defined sadmin configuration file 
($SADMIN/cfg/sadmin.cfg).
{: .text-justify}

[Back to the top](#top_of_page)



<a id="sysmon_error_group"></a>
### Error alert group
Column 'K' represent the Error Alert Group to advise when a error need to be issue. Group MUST 
be defined in the Alert Group File ($SADMIN/cfg/alert_group.cfg). When new filesystem line are 
added the default group used for Warning/Error is the one defined sadmin configuration file 
($SADMIN/cfg/sadmin.cfg).
{: .text-justify}

[Back to the top](#top_of_page)




<br>
<a id="script"></a>
### Running script within SysMon

See the page on 
[how to make the System Monitor run your own script]({% post_url 2021-06-26-sadm-sysmon-script %}).

[Back to the top](#top_of_page)




<br>
<a id="loadaverage"></a>
### Monitoring the system load average

We dedicated a page on [How-to monitor the system average]({% post_url 2021-06-26-sadm-sysmon-load-average %}) with the System Monitor.   

[Back to the top](#top_of_page)




<br>
<a id="cpuusage"></a>
### Monitoring the CPU utilization
See the dedicated page on ["How-to monitor cpu utilization page"]({% post_url 2021-06-26-sadm-sysmon-cpu-usage %})

[Back to the top](#top_of_page)





<br>
<a id="swapspace"></a>
### Check Swap Space utilization

We have create a page on ["Monitoring system swap space"]({% post_url 2021-07-01-sadm-sysmon-swapspace %})

[Back to the top](#top_of_page)




<br>
<a id="http"></a>
### Verify Web site responsiveness

We have create a page on ["Verifying Web site responsiveness"]({% post_url 2021-06-27-sadm-sysmon-https %})

[Back to the top](#top_of_page)




<br>
<a id="service"></a>
### Service Monitoring

**Thing to remember**
- The service name MUST be prefix by the string 'service_'.
- A "1" is returned if the service is active and a "0" if isn't.
- They can be one or multiple service name specified (separated by comma).
- Example, Redhat use 'crond' service name, Ubuntu use 'cron'. 
- To test if the cron daemon is running on both system you specify multiple services.
- Example : service_crond,cron
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

**Example, for testing if a service is running**
- Restart a service or not
  - If you don't want to restart a service if it dies, don't put the service restart service script
 "srestart.sh" at the end of the line (like postfix line). If you do want to restart a service, then
 put "srestart.sh" at the end of the line. Remember that this script is located in the monitor script
 directory "$SADMIN/usr/mon".
- Service may not have the same name on all distributions
  - On RedHat, Fedora, CentOS the cron service is called "crond", on Ubuntu, Debian, Raspbian it is
called "cron". So to deal with that, SysMon allow you to specify the two names separated by comma,
and it will test both of them and as long one these service is up, it will consider it as ok. If
none of them is up and the "srestart.sh" is specified, it will try to restart both of them (but only
one of them will obviously work).
{: .text-justify}

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



<br>
<a id="daemon"></a>
### Daemon running

- Line MUST  begin with "daemon_", followed by the process name (found in a "ps -ef").
- The function search to the specify "name" is present in the process list (ps) of the system. The 
search is case sensitive.
- This test only search for the string following the "daemon_" literal in the process list and 
return the number of time it was found. If it's not found then a "0" is returned, like the code 
below that search for the "gitea" process.  

```bash
$ ps -ef | grep gitea | grep -v grep 
git        501     1  4 Jun25 ?        07:10:09 /home/git/gitea/gitea web
$ count=$(ps -ef | grep gitea | grep -v grep | wc -l)
$ echo $count
1
```

So here if the "gitea" process counted is "0", then it's lower (< col 3) than "1" (col 5) then the
script "gitea.sh" would be executed. 
- Important to remember that after each execution of the script the execution counter (Col 6) is 
incremented by 1 and that each time the process is found in the process list it is set back to "0". 
- It would be not be reasonable to try to restart the process over and over each time System 
Monitor run. So once it as tried to restart it two times, it won't try to restart it again for the 
next 24 hours and an alert is generated. How does System Monitor achieve that you would ask, well 
each time the script is run the date and time of the execution is recorded in column "H" and "I". 
So when the third tries to run the script, the System Monitor calculate the time since the last 
execution and if it's greater than 24 hours, then counter (col 6) is set to one, column "H" and "I" 
set to current date and time, and execution of the script is started.
{: .text-justify}

```bash
#
# ----- Monitor Daemon or Process Running 
# ID COLUMN 1  2  3  4  5   6  7    8   9 A B C D E F G     H     I      J       K    L
daemon_gitea   1  < 00 01 000 0000 0000 Y Y Y Y Y Y Y Y 20180820 1520 default default -
or to restart it with your own script (sgitea.sh)
daemon_gitea   1  < 00 01 000 0000 0000 Y Y Y Y Y Y Y Y 20180820 1520 default default gitea.sh
```

If you decide to execute a script if the System Monitor can find "gitea" in the process list (like
above), your script MUST be place it the directory "$SADMIN/usr/mon". You make a copy of the template
available to you "stemplate.sh"  and create the associated error message file you want to show the
user when your script failed to restart the process. 
{: .text-justify}

```bash
$ cd $SADMIN/usr/mon
$ cp stemplate.sh gitea.sh 
$ echo "Couldn't restart gitea process (gitea.sh)." > gitea.txt
$ vi gitea.sh 
$ chmod +x gitea.sh
```



[Back to the top](#top_of_page)




<br>
<a id="multipath"></a>
### Multipath test

- Again if the [minimum conditions](#sysmon_conditions) are met, then multipath state is evaluated. 
If not we proceed with the next line of Sysmon configuration file.
- Multipath line are only evaluated on Linux.
- Line will only be evaluated if the command 'multipathd' is present on system.
- SysMon check each path of the multipath 
  - If all multipath are active or ready then a "1" is returned (place in column 2).
  - If one one them is not "active" or "ready", a value of 0 is returned.

```bash
# ----- Check Linux Multipath Status (0=Error 1=All path(s) are Online/Ready)
# ID COLUMN 1    2  3   4   5  6    7    8  9 A B C D E F G     H      I     J      K    L
check_multipath  0 !=  00  01 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 warngrp errgrp -
```

In the example above, the multipath test returned a problem ("0" in column 2), since "0" is
not equal (!=) to "1" (Column 5) then an error is generated (Remember that when column 4 or 5 is 
"0" they are ignored). The alert will sent to the error group "errgrp" specify in column
"K". This error group got to be part of the [Alert Group File]({% post_url 2021-06-19-alert-group-cfg %}) 
($SADMIN/cfg/alert_group.cfg).
{: .text-justify}

Example on the command use to verify that multipath are all active/ready :

```bash
# echo 'show paths' | multipathd -k | grep -vi multipath
   0:0:0:0 sda 8:0   1   [active][ready] XX........ 4/20
   0:0:0:1 sdb 8:16  1   [active][ready] XX........ 4/20
   1:0:0:0 sdc 8:32  1   [active][ready] XXXX...... 8/20
   1:0:0:1 sdd 8:48  1   [active][ready] XXXX...... 8/20
```

[Back to the top](#top_of_page)




<br>
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





<br>
<a id="filesystem"></a>
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
# Can increase it by 10%, two times within 24hours maximum, if script 
# "sadm_fs_incr.sh" in Column L.
# FS/usr 23 >= 25 90 001 0000 0000 Y Y Y Y Y Y Y Y 20180615 0824 wargrp errgrp sadm_fs_incr.sh
#----------------------------------------------------------------------------------------
# ID COLUMN 1  2  3   4   5  6   7    8   9 A B C D E F G     H     I     J       K     L
#----------------------------------------------------------------------------------------
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

