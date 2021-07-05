---
title:          Monitoring Services
desc:           How-to monitor services with SysMon
version:        2.44
summary: |         
    On this page we will demonstrate how you can monitor system services with System Monitor and be
    be able to restart them if they are not running.
    {: .text-justify}
updated:        2021-07-05
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

{% include sadm/sadm_page_info.md %}
{% if page.type == "S" %}
<font size="3"><strong>Can only be run on SADMIN Server.</strong></font>
{% endif %}
{% if page.type == "B" %}
<font size="3"><strong>Can be executed on a client and on the SADMIN Server.</strong></font>
{% endif %}


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







<a id="seealso"></a>
## See also

| Link to ...| Description |  
| :--- | :--- |  
| [sadm_sysmon_tui.pl]({% post_url 2021-05-18-sadm-sysmon-tui %})                   |  Command line summary of alerts and failed scripts of all your servers.  
| [sadm_sysmon.pl]({% post_url 2021-06-10-sadm-sysmon %})                           | Client system monitor   
| [sadm_fetch_client.sh]({% post_url 2021-03-16-sadm-fetch-client %})               | rsync all .rch/.log/.rpt from actives clients to the SADMIN server  
| [SysMon configuration file]({% post_url 2021-06-11-sadm-sysmon-config %})         | Client System Monitor configuration file   
| [sadmin.cfg]({% post_url 2021-04-26-sadmin-cfg %})                                | SADMIN main configuration file   

