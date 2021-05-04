---
title:          man_template.sh
desc:           Template for scripts documentation
version:        2.2
updated:        2021-04-22
os:             Linux, Aix, MacOS
type:           B  # [S]=Run on Server only, [C]=Client Only, [B]=Run on Both
tags:           [ test ] 
#categories:     [ web_interface, configuration_files, system_monitor, server_scripts, client-scripts, command_line,  utilities, libraries, templates, test ] 
categories:     [ test ] 
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

The running scripts are listed first, then the scripts that terminated with an error and 
finally all the scripts grouped by system. So it give you view of the statistics of each script 
(start time, end time, elapse time,...) of each systems sorted and grouped by name. When 
something look different than the normal, like the alert group used is different than the 
default group or the last execution date of a script is more than thirty days, it will be 
shown with a yellow background. 
  {: .text-justify}
 
```bash
# include script
```


<a id="examples"></a>
## EXAMPLE

```bash
# Example of script output
```
<!-- ![Daily Script Report Example](/assets/img/man/sadm_daily_report_script.png){: .align-center} -->


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
