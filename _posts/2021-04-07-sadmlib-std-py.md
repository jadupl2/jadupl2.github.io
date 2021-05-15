---
title:          sadmlib_std.py
desc:           SADMIN standard python library
updated:        2021-05-15
version:        3.15
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


## SADMIN Standard library functions

| Function Call |   Description |  Return value example |   
| :---  | :--- | :---  |  
| check_requirements()              | Check/Set Path of require cmd (False if some missing)   | True or False |
| date_to_epoch(self,wd)            |       |       |
| dbclose(self)         |       |       |
| dbconnect(self)           |       |       |
| elapse_time(self,wend,wstart)         |       |       |
| epoch_to_date(self,wepoch)            |       |       |
| get_arch(self)            |       |       |
| get_domainname(self)          |       |       |
| get_epoch_time(self)          |       |       |
| get_fqdn(self)            |       |       |
| get_host_ip(self)         |       |       |
| get_hostname(self)          |       |       |
| get_kernel_bitmode(self)          |       |       |
| get_kernel_version(self)          |       |       |
| get_oscodename(self)          |       |       |
| get_osmajorversion(self)          |       |       |
| get_osminorversion(self)          |       |       |
| get_osname(self)          |       |       |
| get_ostype(self)          |       |       |
| get_osversion(self)           |       |       |
| get_packagetype(self)         |       |       |
| get_release(self)             |       |       |
| get_serial(self)          |       |       |
| __init__(self)            |       |       |
| load_config_file(self,sadmcfg)            |       |       |
| locate_command(self,cmd)          |       |       |
| oscommand(self,command)           |       |       |
| sendmail(server,port,user,pwd,sub,body)            |       |       |
| show_version(self)            |       |       |
| silentremove(self,filename)           |       |       |
| start (self)          |       |       |
| stop(self,return_code)            |       |       |
| trimfile(self,fname, nlines=500)          |       |       |
| writelog(self,sline,stype="normal")           |       |       |




{% include {{ site.section_environment }} %}

{% include {{ site.section_exitcode    }} %}

{% include {{ site.section_author      }} %}

{% include {{ site.section_copyright   }} %}


<a id="seealso"></a>
## SEE ALSO

[sadmlib_std.sh ]({% post_url 2021-04-07-sadmlib-std-sh %}) - SADMIN standard shell library  
[sadmlib_screen.sh ]({% post_url 2019-10-12-sadmlib-screen-sh %}) - SADMIN screen oriented library  
[sadm_template.sh]({% post_url 2021-03-16-sadm-template-sh %}) - Using SADMIN Shell script template   
[sadm_template.py]({% post_url 2021-03-16-sadm-template-py %}) - Using SADMIN Python script template    
[sadm_template_menu.sh]({% post_url 2021-04-30-sadm-template-menu %}) - Using SADMIN shell menu template   
[sadmlib_std_demo.sh]({% post_url 2019-10-12-sadmlib-std-demo-sh %}) - SADMIN Shell Library Functions Demo   
[sadmlib_std_demo.py]({% post_url 2019-10-12-sadmlib-std-demo-py %}) - SADMIN Python Library Functions Demo  


