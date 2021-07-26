---
title:          Verify Web site responsiveness
desc:           How-to monitor Web site responsiveness
version:        2.45
summary: |         
    On this page we will demonstrate how you can monitor web site is responsive or not to an 'http'
    or a 'https' request.
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


<a id="http_https"></a>
### Verify Web site responsiveness

- With the System Monitor you can verify if a web site is responsive or not to an 'http' or a 'https'
request. To monitor if a web site is reponsive to a 'http' or 'https' request, you must insert a 
line in SysMon configuration file ($SADMIN/cfg/`hostname-s`.smon) like the one below. The line MUST 
begin with the string "http_" or "https_". The System monitor is using the "curl http(s):sitename -I"
to check the site responsiveness.
- As always column two represent the result of the test, so we will have a '0' if we can connect to 
the web site and a '1' if we can't.
{: .text-justify}


In the example below, the web site "http://coco.coco" didn't respond (1 in column 2) and the one
web site did respond to request. When a web site don't respond to the request, then an alert is 
issue to the "Error" alert group, since the error is activated by the '1' in column 5 (Error 
Threshold). Remember, when we have a '00' in column 4 (Warning threshold) or 5 (Error threshold) the
value (column 2) is not tested against it. 
{: .text-justify}

```bash
#
# Test web site responsiveness (0=OK 1=NoResponse)
# ID COLUMN 1       2 3  4  5  6   7    8   9 A B C D E F G     H     I     J       K     L
https_sadmin.ca     0 = 00 01 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 default default -
https_linternux.com 0 = 00 01 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 default default -
https_site.com:3001 0 = 00 01 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 default default -
#
```


<br>
**Example of SysMon output**  

In the example two out of three web sites did response and one that didn't (http://coco.coco). 

```bash
# sadm_sysmon.pl
root@holmes:~ # sadm_sysmon.pl

Creating lock file /sadmin/sysmon.lock
Loading SADMIN configuration file /sadmin/cfg/sadmin.cfg
------------------------------------------------------------------------------
SADMIN SYStem MONitor Tools - Version 2.44
------------------------------------------------------------------------------
O/S Name                 = linux
Debugging Level          = 5
SADM_BASE_DIR            = /sadmin
Hostname                 = holmes
Virtual Server           = N
CMD_SSH                  = /bin/ssh
------------------------------------------------------------------------------
...
...

Checking response from http://coco.coco ... 
[ ERROR ] (6) Web site not responding
Error #6 : Could not resolve host name

Checking response from https://sadmin.ca ... 
[OK] Web site is responding

Checking response from https://linternux.com ... 
[OK] Web site is responding
...
...
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

