---
title:          Monitoring daemon (process)
desc:           How-to monitor daemon (process) on a system with SysMon
version:        2.44
summary: |         
    On this page we will demonstrate how you can monitor if a daemon (process) in running on a system.
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


<a id="daemon"></a>
### Daemon running

- Line MUST  begin with "daemon_", followed by the process name (found in a "ps -ef").
- The function search to the specify "name" is present in the process list (ps) of the system and
the search is case sensitive.
- This test only search for the string following the "daemon_" literal in the process list and 
return the number of time it was found. If it's not found then a "0" is returned, like the code 
below that search for the "gitea" process.  

```bash
$ ps -ef | grep gitea | grep -v grep 
git        501     1  4 Jun25 ?        07:10:09 /home/git/gitea/gitea web
$ echo $(ps -ef | grep gitea | grep -v grep | wc -l)
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







<a id="seealso"></a>
## See also

| Link to ...| Description |  
| :--- | :--- |  
| [sadm_sysmon_tui.pl]({% post_url 2021-05-18-sadm-sysmon-tui %})                   |  Command line summary of alerts and failed scripts of all your servers.  
| [sadm_sysmon.pl]({% post_url 2021-06-10-sadm-sysmon %})                           | Client system monitor   
| [sadm_fetch_clients.sh]({% post_url 2021-03-16-sadm-fetch-clients %})               | rsync all .rch/.log/.rpt from actives clients to the SADMIN server  
| [SysMon configuration file]({% post_url 2021-06-11-sadm-sysmon-config %})         | Client System Monitor configuration file   
| [sadmin.cfg]({% post_url 2021-04-26-sadmin-cfg %})                                | SADMIN main configuration file   

