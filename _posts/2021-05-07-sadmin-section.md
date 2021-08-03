---
title:          SADMIN Section of script
permalink:      /sadm-section/
desc:           SADMIN code section to include in your script.
version:        1.50
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


<a id="description_shell"></a>
## Code section for Shell script

The code below MUST appear in the beginning of every shell scripts using the SADMIN tools. You must
also call at the beginning of your script the '[sadm_start()]({% post_url 2019-10-12-sadmlib-std-demo-sh %}/#sadm_start)' 
function and the '[sadm_stop()]({% post_url 2019-10-12-sadmlib-std-demo-sh %}/#sadm_stop)' function
at the end of your script before it finish.
{: .text-justify}

{% include sadm/sadm_section_sh.md %}



<a id="description_python"></a>
## Code section for Python script

The code below MUST appear in the beginning of every Python scripts using the SADMIN tools. You must
also call at the beginning of your script the '[setup_sadmin()]({% post_url 2019-10-12-sadmlib-std-demo-py %}/#start_stop_module)'
function. This function include the call to the 'st.start()', so you don't have to worry about 
calling it. But before the end of your script you MUST call the 'st.close(exitcode)'.
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
