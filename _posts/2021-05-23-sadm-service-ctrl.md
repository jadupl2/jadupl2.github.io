---
title:          sadm_service_ctrl.sh
desc:           Enable, disable & get status of system startup and shutdown script
version:        2.10
updated:        2021-05-23
os:             Linux
type:           B  # [D]oc [S]=Server only [C]=Client [B]oth
tags:           [ utilities ] 
categories:     [ utilities ] 
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
{{ page.title }} [-d 0-9] [-h] [-l] [-s] [-u] [-v] 
```
{% if page.type == "S" %}
<font size="3"><strong>Can only be run on SADMIN Server.</strong></font>
{% endif %}
{% if page.type == "B" %}
<font size="3"><strong>Can be executed on a client and on the SADMIN Server.</strong></font>
{% endif %}




<a id="description"></a>
## DESCRIPTION

Script is use to **set** (enable), **unset** (disable) and **list** the status of SADMIN Service. 
When SADMIN service is enable, the following scripts are executed at system startup and shutdown.
{: .text-justify}

    At system startup  : $SADMIN/sys/sadm_startup.sh
    At system shutdown : $SADMIN/sys/sadm_shutdown.sh

When the SADMIN service is unset (disable), these scripts are not executed. You can get the status 
of SADMIN service, by using the '-l' command line option. This service support 'Systemd' and 
System V Init (SysV) scheme. As usual these scripts produce log and they can be looked at in 
"$SADMIN/log", if there is a need to.
{: .text-justify}


**Scripts use for the SADMIN service itself are:**
- For System V Init SADMIN use the template file '$SADMIN/cfg/.sadmin.rc'  
- For Systemd SADMIN use the template file '$SADMIN/cfg/.sadmin.service'  

These files are use by this script to construct the SADMIN service. You don't need to modify these 
files, they could modified by future update. 
{: .text-justify}
 
[Back to the top](#top_of_page)



<a id="examples"></a>
## EXAMPLE

### Set/Enable the SADMIN service
```bash
# sadm_service_ctrl.sh -s
cp /sadmin/cfg/.sadmin.service /etc/systemd/system/sadmin.service ... [OK]
systemctl enable sadmin.service ... [OK]
systemctl stop sadmin.service ... [OK]
systemctl start sadmin.service ... [OK]
systemctl status sadmin.service ... [ OK ]
sadmin.service                                enabled 

Consequence of enabling SADMIN service :
/sadmin/sys/sadm_startup.sh, will be executed at system startup.
/sadmin/sys/sadm_shutdown.sh will be executed on system shutdown.
We encourage you to customize these two scripts to your need.
#
```

### Unset/Disable the SADMIN service
```bash
# sadm_service_ctrl.sh -u
systemctl stop sadmin.service ... [OK]
systemctl disable sadmin.service...[OK]
rm -f /etc/systemd/system/sadmin.service ...[OK]

Consequence of disabling SADMIN service :
/sadmin/sys/sadm_startup.sh, will not be executed at system startup.
/sadmin/sys/sadm_shutdown.sh will not be executed on system shutdown.
# 
```


### List the status of the SADMIN service
You can also use the command 'systemctl status sadmin' on System system.
```bash
# sadm_service_ctrl.sh -l
systemctl status sadmin.service ... [ OK ]
sadmin.service                                enabled 
# 
```
<!-- ![Daily Script Report Example](/assets/img/man/sadm_daily_report_script.png){: .align-center} -->

[Back to the top](#top_of_page)


{% include {{ site.section_options     }} %}
| **-l** | List/Display the status of the SADMIN service | 
| **-s** | Set/Enable execution of startup & shutdown script | 
| **-u** | Unset/Disable execution of startup & shutdown script| 


{% include {{ site.section_environment }} %}

{% include {{ site.section_exitcode    }} %}

{% include {{ site.section_author      }} %}

{% include {{ site.section_copyright   }} %}


<a id="seealso"></a>
## SEE ALSO

[sadm_push_sadmin.sh]({% post_url 2021-05-22-sadm-push-sadmin %}) - Push SADMIN version to one or all actives clients. 
