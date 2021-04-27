---
title:          man_template.sh
desc:           Template for scripts documentation
version:        2.2
date:           2021-01-01
updated:        2021-04-22
os:             Linux, Aix, MacOS
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
  title: "Documentation"
  nav: sidebar-manpage
---

<font size="3">
<div>$SADMIN/bin/{{ page.title }}</div>
<div>Version v{{ page.version }} - Updated {{ page.updated }}</div>
<div>Run on {{ page.os }}</div>
</font>


<a id="name"></a>

## NAME
{{ page.title }} -- {{ page.desc }}


<a id="synopsis"></a>

## SYNOPSIS

```bash
    {{ page.title }} [-v] [-h] [-d 0-9]  
```


<a id="description"></a>

## DESCRIPTION

<!-- ![Daily Script Report Example](/assets/img/man/sadm_daily_report_script.png){: .align-center} -->
  - The running scripts are listed first, then the scripts that terminated with an error and 
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


{% include {{ site.section_options     }} %}

{% include {{ site.section_environment }} %}

{% include {{ site.section_exitcode    }} %}

{% include {{ site.section_author      }} %}

{% include {{ site.section_copyright   }} %}


<a id="seealso"></a>

## SEE ALSO
[The Daily Backup Script - sadm_backup.sh](#)
