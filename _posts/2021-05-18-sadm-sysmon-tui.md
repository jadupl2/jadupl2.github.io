---
title:          sview (sadm_sysmon_tui.pl)
permalink:      /sadm-sysmon-tui/
desc:           System monitor viewer from command line
version:        2.0
updated:        2021-05-19
os:             Linux, Aix, MacOS
type:           S  # [D]oc [S]=Server only [C]=Client [B]oth
tags:           [ command_line ] 
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

<a id="top_of_page"></a>
{% include sadm/sadm_page_info.md %}

<a id="name"></a>
## NAME
**{{ page.title }}** - *{{ page.desc }}*   



<a id="synopsis"></a>
## SYNOPSIS

```bash
{{ page.title }} 
```
{% if page.type == "S" %}
<font size="3">Can only be run on SADMIN Server.</font>
{% endif %}



<a id="description"></a>
## DESCRIPTION

This script summarize all alerts coming from the SADMIN system monitor and will show you a 
list of errors and warning encountered with the scripts run by all your systems. The screen 
automatically refresh every 10 seconds. This script doesn't need 'root' privilege and can be run 
by any users part of the "sadmin' group.
{: .text-justify}
 
```bash
$ sview 
```


<a id="examples"></a>
## EXAMPLE

![sview (sadm_sysmon_tui.pl)](/assets/img/man/sadm_sysmon_tui.png){: .align-center}


{% include {{ site.section_environment }} %}

{% include {{ site.section_exitcode    }} %}

{% include {{ site.section_author      }} %}

{% include {{ site.section_copyright   }} %}


<a id="seealso"></a>
## SEE ALSO

[sadm_fetch_clients.sh]({% post_url 2021-03-16-sadm-fetch-clients %}) - rsync all .rch/.log/.rpt from actives clients to the SADMIN server.  
[sadmlib_std_demo.sh]({% post_url 2019-10-12-sadmlib-std-demo-sh %}) - SADMIN shell library functions demo   
[sadmlib_std_demo.py]({% post_url 2019-10-12-sadmlib-std-demo-py %}) - SADMIN python library functions demo  
[SADMIN installation](/_pages/install) - SADMIN installation page. 