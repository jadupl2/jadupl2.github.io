---
title:          sadm_show_rch.sh
desc:           Show Result History files (.rch) from all systems.
version:        1.18 
updated:        2021-05-05
os:             Linux, Aix (Server only)
type:           S  # [S]=Run on Server only, [C]=Client Only, [B]=Run on Both
tags:           [ command_line, tools, result_code_history(rch) ]
categories:     [ command_line ] 
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

<font size="3">
<div>$SADMIN/bin/{{ page.title }}</div>
<div>Version v{{ page.version }} - 
Posted {{ page.date | date: "%Y-%m-%d" }} - 
Updated {{ page.updated }}</div>
<div>Run on {{ page.os }}</div>
</font>


<a id="name"></a>

## NAME
**{{ page.title }}** - ***{{ page.desc }}***   
*The alias command "**srch**" can be use instead of {{ page.title }}*



<a id="synopsis"></a>

## SYNOPSIS

```bash
    {{ page.title }} [-v] [-h] [-d 0-9] [-s server-name] [-p] [-w] [-m]  
```
{% if page.type == "S" %}
<font size="3">Can only be run on SADMIN Server.</font>
{% endif %}



<a id="description"></a>

## DESCRIPTION

Show the actual status of every scripts of all your systems. The information presented by this 
scripts, is collected from all your servers every 5 minutes by the "sadm_fetch_clients.sh" script. 
The running script (if any) are presented first, followed by the script(s) that ended with error 
and finally the script that ended with success, sorted by descending date and time. *This command 
can be executed only on the SADMIN server.*
 {: .text-justify}


<a id="examples"></a>

## EXAMPLE

```# srch```  
![Show RCH Main Screen](/assets/img/man/sadm_show_rch.png){: .align-center}  


Example of the RCH Summary Report for a specific server   

```# srch -s raspi6```   
![Show RCH for one server](/assets/img/man/sadm_show_rch-s.png){: .align-center}  


Example to watch the RCH Summary Report first page in real time (Refresh every 60 seconds)  

```# srch -w```  
![Watch RCH in real time](/assets/img/man/sadm_show_rch-w.png){: .align-center}  


View the RCH Summary Report without stopping at each page (nopage).  

```# srch -p```  
![List RCH without stopping at each page](/assets/img/man/sadm_show_rch-p.png){: .align-center}  


Send a mail of the RCH Summary Report so to 
[email address specify in $SADMIN/cfg/sadmin.cfg]({% post_url 2021-04-26-sadmin-cfg %}#sadm_mail_addr).  

```# srch -m```  
![Mail Today and yesterday RCH Report](/assets/img/man/sadm_show_rch-m.png){: .align-center}  


Example of email sent 
![Mail Sent](/assets/img/man/sadm_show_rch-m2.png){: .align-center}  


{% include {{ site.section_options     }} %}
| **-s [Server]** | Show the RCH Summary Report for the server specified.|
| **-m** | Send the RCH Summary Report to SysAdmin email.| 
| **-w** | Watch the RCH Summary Report in real time (Updated every 60 Sec.). |
| **-p** | Show the RCH Summary Report without paging. |

{% include {{ site.section_environment }} %}

{% include {{ site.section_exitcode    }} %}

{% include {{ site.section_author      }} %}

{% include {{ site.section_copyright   }} %}


<a id="seealso"></a>
## SEE ALSO

[SADMIN installation](/_pages/install) - SADMIN installation page.    
