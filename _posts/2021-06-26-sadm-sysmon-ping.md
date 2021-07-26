---
title:          Ping system test
desc:           How-to monitor respond to a ping test
version:        2.44
summary: |         
    On this page we will demonstrate how you can monitor the reponse to a ping test.
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






<a id="seealso"></a>
## See also

| Link to ...| Description |  
| :--- | :--- |  
| [sadm_sysmon_tui.pl]({% post_url 2021-05-18-sadm-sysmon-tui %})                   |  Command line summary of alerts and failed scripts of all your servers.  
| [sadm_sysmon.pl]({% post_url 2021-06-10-sadm-sysmon %})                           | Client system monitor   
| [sadm_fetch_clients.sh]({% post_url 2021-03-16-sadm-fetch-clients %})               | rsync all .rch/.log/.rpt from actives clients to the SADMIN server  
| [SysMon configuration file]({% post_url 2021-06-11-sadm-sysmon-config %})         | Client System Monitor configuration file   
| [sadmin.cfg]({% post_url 2021-04-26-sadmin-cfg %})                                | SADMIN main configuration file   

