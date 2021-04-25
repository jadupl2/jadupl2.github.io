---
title:          man_template.sh
desc:           Template for scripts documentation
date:           2021-01-01
updated:        2021-04-22
modified:       2021-04-22
os:             Linux, Aix, MacOS
layout:         single
search:         true
tags:           [ test ] 
#categories:     [ Web Interface, System Monitor, Automated Server Scripts, Automated Client Scripts, Command Line Tools,  Utilities, Libraries, Templates, Test ] 
categories:     [ test ] 
author_profile: false
toc:            false
classes:        wide
sidebar:
  title: "Documentation"
  nav: sidebar-manpage
---

<font size="3">
<div>$SADMIN/bin/{{ page.title }}</div>
<div>Updated {{ page.updated }}</div>
<div>Run on {{ page.os }}</div>
</font>


### NAME

{{ page.title }} -- {{ page.desc }}


### SYNOPSIS

{% highlight bash %}
    sadm_daily_report.sh [-v] [-h] [-b] [-r] [-s] [-d 0-9]  
    ls [-ABCFGHLOPRSTUW@abcdefghiklmnopqrstuwx1%] [file ...]
{% endhighlight %}


### DESCRIPTION

The script produce ...
<!-- ![Daily Script Report Example](/assets/img/man/sadm_daily_report_script.png){: .align-center} -->
  - The running scripts are listed first, then the scripts that terminated with an error and finally all the scripts grouped by system. So it give you view of the statistics of each script (start time, end time, elapse time,...) of each systems sorted and grouped by name. When something look different than the normal, like the alert group used is different than the default group or the last execution date of a script is more than thirty days, it will be shown with a yellow background. 
  {: .text-justify}
 
```bash
# include script
```



### EXAMPLE

```bash
```

<a id="options"></a>
### OPTIONS

| Options | Description                                |
|:-------:|:------------------------------------------ |
| **-d**  | Set Debug level from 0 to 9 (Default is 0) |
| **-h**  | Display this help and exit.                |
| **-v**  | Output version information and exit.       |


### ENVIRONMENT
The following environment variables affect the execution of {{ page.title }}:  
- **"$SADMIN"** environment variable specify the root directory of the SADMIN tools (normally /opt/sadmin).  
  - It should be already done, the setup script have updated the /etc/profile.d/sadmin.sh and then /etc/environment files.  
- The [SADMIN main configuration file](/doc/man/file_sadmin_cfg.php), is needed and it's loaded in memory at the beginning of every scripts.
  - This file should already exist and contains your SADMIN configuration and preference setting.
- SADMIN Tools shell library, "$SADMIN/lib/sadmlib.sh".  


### EXIT STATUS

| Exit Code | Description                                             |
| :-------: | :----------------                            ~~~~           |
| 0         | An exit status of zero indicates success.               |  
| 1         | Failure is indicated by a nonzero value, typically ‘1’. |  


### AUTHOR
[Jacques Duplessis](jacques.duplessis@sadmin.ca.)  
Any suggestions or bug report can be submitted at the [support page](www.sadmin.ca/support.php)


### COPYRIGHT
Copyright © 2021 Free Software Foundation, Inc. License GPLv3+: [GNU GPL version 3 or later](http://gnu.org/licenses/gpl.html)  
This is free software, you are free to change and redistribute it.   
There is NO WARRANTY to the extent permitted by law.  


### SEE ALSO
The Daily Backup Script - [sadm_backup.sh](#)
