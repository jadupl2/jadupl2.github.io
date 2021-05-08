---
title:          SADMIN Section of script
desc:           SADMIN code section to include in your script.
version:        2.2
updated:        2021-05-07
os:             Linux, Aix, MacOS
type:           D  # [D]oc [S]=Server only [C]=Client [B]oth
tags:           [ libraries ] 
categories:     [ libraries ] 
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


<a id="description"></a>
## DESCRIPTION

The running scripts are listed first, then the scripts that terminated with an error and 
finally all the scripts grouped by system. So it give you view of the statistics of each script 
(start time, end time, elapse time,...) of each systems sorted and grouped by name. When 
something look different than the normal, like the alert group used is different than the 
default group or the last execution date of a script is more than thirty days, it will be 
shown with a yellow background. 
{: .text-justify}

{% include sadm/sadm_section_sh.md %}



<a id="description"></a>
## DESCRIPTION

The running scripts are listed first, then the scripts that terminated with an error and 
finally all the scripts grouped by system. So it give you view of the statistics of each script 
(start time, end time, elapse time,...) of each systems sorted and grouped by name. When 
something look different than the normal, like the alert group used is different than the 
default group or the last execution date of a script is more than thirty days, it will be 
shown with a yellow background. 
{: .text-justify}

{% include sadm/sadm_section_py.md %}


{% include {{ site.section_environment }} %}

{% include {{ site.section_author      }} %}

{% include {{ site.section_copyright   }} %}


<a id="seealso"></a>
## SEE ALSO

[sadm_requirements.sh]({% post_url 2019-03-21-sadm-requirements %}) - List/Install required SADMIN Tools packages  
[sadm_template.sh]({% post_url 2021-03-16-sadm-template-sh %}) - Using SADMIN Shell script template   
[sadm_template.py]({% post_url 2021-03-16-sadm-template-py %}) - Using SADMIN Python script template    
[sadmlib_std_demo.sh]({% post_url 2019-10-12-sadmlib-std-demo-sh %}) - SADMIN Shell Library Functions Demo   
[sadmlib_std_demo.py]({% post_url 2019-10-12-sadmlib-std-demo-py %}) - SADMIN Python Library Functions Demo  
