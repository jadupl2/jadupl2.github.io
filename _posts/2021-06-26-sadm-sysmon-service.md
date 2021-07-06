---
title:          Monitoring Services
desc:           How-to monitor services with SysMon
version:        2.44
summary: |         
    With System Monitor you can check if a particular service is running, it can also restart it if
    you wish. It will try to start it two times, it it can't it will then send an alert to the
    group of your choice.
    {: .text-justify}
updated:        2021-07-06
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

{{ page.summary }} 

**Thing to remember**
- When you want to monitor a service, the ***line must begin with the string "service_", 
followed by the service(s) name(s)***. Service doesn't have the same name on all distributions, on RedHat, 
Fedora, CentOS the cron service is called "crond", on Ubuntu, Debian, Raspbian it is called "cron". 
So to deal with that, SysMon allow you to specify the two service name separated by comma,
and it will test both of them and as long one these service is up, it will consider it as ok. If
none of them is up and that "srestart.sh" is specified (last field on the line), it will try to 
restart both of them (but only one of them will obviously work).
{: .text-justify}

- As always, the column two contain the result of test, a "1" is returned when the service is active and a "0" if it's down.
- The Sysmon configuration file that is installed initially come with some basic service, but feel
free to add your own or deactivate the one you don't want to use by putting a "#" in column one or
put a "N" in column 'G'.

### Restarting a service
- When a service is down, SysMon can run one of your script or used the one that come with SADMIN ($SADMIN/usr/mon/srestart.sh) to bring it up.
  - You put the restart script in the last column (column L) of the line, to get executed.
  - Script name must exist in '$SADMIN/usr/mon' directory and be executable. 
  - If the service is down the script is executed, but no more than twice in a 24 Hrs period. This prevent Sysmon from trying to restart the service every five minutes.
    - SADMIN SysMon does this by looking at column 6 (RunCounter) and the event date and time (column H & I).
    - The H and the I fields contain the date and time of the last script execution.
    - The Column 6 contain the number of time the script ran in the last 24 hrs.
    - With this information SysMon can know if it was run in the last 24 hours. 
    - If it wasn't run in the last 24 Hrs, the RunCounter(Col 6) is reset to 1 and the script executed. 
    - If the script was executed in the last 24Hrs and the RunCounter is less than 2, then the script is executed. 
    - If the script was executed in the last 24Hrs and the RunCounter is greater than 2, the script isn't executed, since it already ran twice in the last 24 hours.


<br>
- **Restart a service or not**
  - If you don't want to restart a service if it dies, don't put the service restart service script
 "srestart.sh" at the end of the line (like postfix line). If you do want to restart a service, then
 put "srestart.sh" at the end of the line. *Remember that every script specify in column L, got to 
 be in directory "$SADMIN/usr/mon"*.

- **Service may not have the same name on all distributions**
  - On RedHat, Fedora, CentOS the cron service is called "crond" and the sss service "sshd", on 
Ubuntu, Debian, Raspbian they are called "cron" and "ssh". So to deal with that kind of situation, 
SysMon allow you to specify the two names separated by comma and it will test both of them. 
When one these service is up, it will consider it as ok. If none of them is up and the "srestart.sh" 
is specified, it will try to restart both of them (but only one of them will obviously work).
{: .text-justify}


### Sample of service section of SysMon configuration file
```bash
#
# ----- Linux Common Service Monitoring
# ID COLUMN 1       2 3  4  5  6    7    8  9 A B C D E F G     H     I      J       K       L
service_crond,cron  1 < 00 01 000 0000 0000 Y Y Y Y Y Y Y Y 20180820 1520 default default srestart.sh
service_chronyd     1 < 00 01 000 0000 0000 Y Y Y Y Y Y Y Y 20180820 1520 default default srestart.sh
service_ssh,sshd    1 < 00 01 000 0000 0000 Y Y Y Y Y Y Y Y 20180820 1520 default default srestart.sh
service_postfix     1 < 00 01 000 0000 0000 Y Y Y Y Y Y Y Y 20180820 1520 default default - 
service_atd         1 < 00 01 000 0000 0000 Y Y Y Y Y Y Y Y 20180820 1520 default default srestart.sh
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

