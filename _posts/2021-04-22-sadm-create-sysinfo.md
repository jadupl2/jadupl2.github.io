---
title:          sadm_create_sysinfo.sh
desc:           Collect hardware & software information about the system
version:        3.21 
updated:        2021-05-08
os:             Linux, Aix, MacOS
type:           C  # [D]oc [S]=Server only [C]=Client [B]oth
tags:           [ client-scripts, web_interface ] 
categories:     [ client-scripts ] 
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

{% include sadm/sadm_page_info.md %}

<a id="name"></a>
## NAME
**{{ page.title }}** - *{{ page.desc }}*   



<a id="synopsis"></a>
## SYNOPSIS

```bash
{{ page.title }} [-d 0-9] [-h] [-v]
```
{% if page.type == "S" %}
<font size="3">Can only be run on SADMIN Server.</font>
{% endif %}



<a id="description"></a>
## DESCRIPTION

When you run this script, no question is asked and files in the disaster recovery directory are updated. This script is part of the 'Client Sunset script' 
(${SADMIN}/bin/sadm_client_sunset.sh). The 'Client Sunset script' is scheduled to run daily from the client crontab (/etc/cron.d/sadm_client). You can also run it manually whenever you want.
{: .text-justify}


<a id="examples"></a>
## EXAMPLE

![sadm_create_sysinfo.png](/assets/img/sadm_create_sysinfo_script.png){: .align-center}

Information in the Disaster Recovery directory, will be useful in case of complete system rebuild. Files in this directory ($SADMIN/dat/dr) are updated daily.

![sadm_create_sysinfo_files.png](/assets/img/sadm_create_sysinfo_files.png){: .align-center}

To view information generated from this script, choose the server to want and click on the buttons on the top of the page..
![sadm_create_sysinfo_web_buttons.png](/assets/img/sadm_create_sysinfo_web_buttons.png){: .align-center}

This is an example of what you would get by pressing the 'Server Summary' button.
![sadm_create_sysinfo_web_info.png](/assets/img/sadm_create_sysinfo_web_info.png){: .align-center}



 

{% include {{ site.section_options     }} %}
| **-i** | Example | 

{% include {{ site.section_environment }} %}

{% include {{ site.section_exitcode    }} %}

{% include {{ site.section_author      }} %}

{% include {{ site.section_copyright   }} %}


<a id="seealso"></a>
## SEE ALSO

[sadm_fetch_client.sh]({% post_url 2021-03-16-sadm-fetch-client %}) - rsync all .rch/.log/.rpt from actives clients to the SADMIN Server.     
[sadm_requirements.sh]({% post_url 2019-03-21-sadm-requirements %}) - List/Install required SADMIN Tools packages  
[sadm_template.sh]({% post_url 2021-03-16-sadm-template-sh %}) - Using SADMIN Shell script template   
[sadm_template.py]({% post_url 2021-03-16-sadm-template-py %}) - Using SADMIN Python script template    
[sadm_template_menu.sh]({% post_url 2021-04-30-sadm-template-menu %}) - Using SADMIN shell menu template   
[sadm_wrapper.sh]({% post_url 2018-02-11-sadm-wrapper %}) - Use to run your existing scripts & benefit of SADMIN tools  
[sadmlib_std_demo.sh]({% post_url 2019-10-12-sadmlib-std-demo-sh %}) - SADMIN Shell Library Functions Demo   
[sadmlib_std_demo.py]({% post_url 2019-10-12-sadmlib-std-demo-py %}) - SADMIN Python Library Functions Demo  
[SADMIN installation](/_pages/install) - SADMIN installation page.    
