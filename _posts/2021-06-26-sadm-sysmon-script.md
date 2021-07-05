---
title:          Running script within SysMon
desc:           Running script within the System Monitor.
version:        2.44
summary: |         
    On this page we will demonstrate how you can make the System MOnitor run one of your custom 
    script and react to exit of it. Like for example, you may have a custom script to check if an application is running or not by issuing special command. If you want to get alerted when it's  not then could or you can even run another script that would restart it for you. Keep reading we will demonstrate all of this with example.
    {: .text-justify}
updated:        2021-07-04
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
<br>
{{ page.summary }} 





<a id="script"></a>
### Running script within SysMon

The System Monitor may noy have the feature you may need. But wait, it can ran a script of your own 
and the result (exit code) be evaluated by SysMon, you can even get alerted if you want when you 
script exit with a non zero code.

- Line MUST begin with "script:" and followed by the script name.
- The script MUST reside in $SADMIN/usr/mon directory and be executable.
- The script will produce a log in that same directory, with the same name as your script.
- Try to get the script execution time as low as possible, remember SysMon run every 5 minutes.
- The script exit code must be '0' when it finish with success and '1' when it fail.
- By default, unless you create it within your script, the error message returned to the user should
be defined in the same directory of your script and have the same name of your script, but with a 
"txt" extension. So if your script name is "stemplate.sh", the error message file would be named 
"stemplate.txt".


**The sample script template**
To demonstrate how to use the "script:" line, we will use the script below, that is supplied and 
that is present in "$SADMIN/usr/mon" directory.

```bash
[/sadmin/usr/mon]: ./stemplate.sh
--------------------------------------------------------------------------------
Starting script stemplate.sh on holmes Sat Jul  3 10:30:01 EDT 2021
Test if file /tmp/sysmon.tmp exist ...
File /tmp/sysmon.tmp doesn't exist
Return code : 1
End of script stemplate.sh on holmes Sat Jul  3 10:30:01 EDT 2021
--------------------------------------------------------------------------------

[/sadmin/usr/mon]: touch /tmp/sysmon.tmp
[/sadmin/usr/mon]: ./stemplate.sh
 
--------------------------------------------------------------------------------
Starting script stemplate.sh on holmes Sat Jul  3 10:30:18 EDT 2021
Test if file /tmp/sysmon.tmp exist ...
File /tmp/sysmon.tmp exist
Return code : 0
End of script stemplate.sh on holmes Sat Jul  3 10:30:18 EDT 2021
--------------------------------------------------------------------------------
```

Let's say we have a line like the one below and we run the System Monitor
```bash
# Run specific scripts, check return code and issue a warning or error based on threshold
# ID - COLUMN 1      2  3   4  5  6    7   8   9 A B C D E F G     H     I     J     K     L
script:stemplate.sh  1  =  00 01 000 0000 0000 Y Y Y Y Y Y Y Y 20180911 1520 wargrp default -
#
```

As part of the output, you will get a message like this on the screen, when the file "/tmp/sysmon.tmp" 
exist.
```bash
# sadm_sysmon.pl
...
Execution of script /sadmin/usr/mon/stemplate.sh is requested
Running script /sadmin/usr/mon/stemplate.sh ... 
Return code is 0
...
```

If we remove the file "/tmp/sysmon.tmp" and we run SysMon again, this time we get an error.
```bash
[/sadmin/usr/mon]: rm -f /tmp/sysmon.tmp
[/sadmin/usr/mon]: sadm_sysmon.pl
...

Execution of script /sadmin/usr/mon/stemplate.sh is requested
Running script /sadmin/usr/mon/stemplate.sh ... 
Return code is 1
Using message in /sadmin/usr/mon/stemplate.txt for rpt file
...
```

**SysMon generated report file** 
```bash
# cat $SADMIN/dat/rpt/holmes.rpt
Error;holmes;2021.07.03;11:25;SCRIPT;stemplate;File /tmp/sysmon.tmp doesn't exist - Running stemplate.sh.;default;default
#
```

**Script error text message file**   
```bash
/sadmin/usr/mon # cat stemplate.txt
File /tmp/sysmon.tmp doesn't exist - Running stemplate.sh.
```

**What user will see on the web interface**   
![SysMon Script Report Example](/assets/img/sadm_sysmon/sadm_sysmon_script.png){: .align-center}


**Email Alert Received**   
Because my error group (column K) was 'default' and it was assign to email in (alert_group.cfg) I
received the email below
![SysMon Script Report Example](/assets/img/sadm_sysmon/sadm_sysmon_script_mail.png){: .align-center}


**You can always check the log of your script execution**
```bash
[/sadmin/usr/mon]: cat stemplate.log
 
--------------------------------------------------------------------------------
Starting script stemplate.sh on holmes Sat Jul  3 10:52:02 EDT 2021

Test if file /tmp/sysmon.tmp exist ...
File /tmp/sysmon.tmp doesn't exist
Return code : 1
 
End of script stemplate.sh on holmes Sat Jul  3 10:52:02 EDT 2021
--------------------------------------------------------------------------------
[/sadmin/usr/mon]: 
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

