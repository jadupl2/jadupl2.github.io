---
title:          sadmlib_std.sh
desc:           SADMIN standard shell library
updated:        2021-05-09
version:        3.69
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
| $(sadm_get_release)                       | Return SADMIN Release Number                          | 1.2.9 |
| $(sadm_get_ostype)                        | Return OS type in uppercase (LINUX,AIX,DARWIN)        |  LINUX |
| $(sadm_get_osversion)                     | Return O/S version (Ex: 7.2, 6.5)                     | 7.9.2009 |
| $(sadm_get_osmajorversion)                | Return O/S major version (Ex 7, 6)                    |  7 |
| $(sadm_get_osminorversion)                | Return O/S minor version (Ex 2, 3)                    |  9  |
| $(sadm_get_osname)                        | Return Uppercase O/S name (REDHAT,CENTOS,UBUNTU,..)   |  CENTOS |
| $(sadm_get_oscodename)                    | Return O/S project code name                          | focal |
| $(sadm_get_kernel_version)                | Return O/S kernel version                             | 5.4.0-58-generic |
| $(sadm_get_kernel_bitmode)                | Return O/S kernel bit mode (32 or 64)                 |  64 |
| $(sadm_get_hostname)                      | Return current host name                              | imac |
| $(sadm_get_host_ip)                       | Return current host IP address                        | 192.168.1.8 |
| $(sadm_get_domainname)                    | Return current host domain name                       | maison.ca |
| $(sadm_get_fqdn)                          | Return fully qualified domain host name               | imac.maison.ca |
| $(sadm_get_epoch_time)                    | Return the current epoch time                         | 1609808693 |
| $(sadm_epoch_to_date 1609808693)          | Convert epoch time to date                            | 2021.01.4 20:04:53 |
| $(sadm_date_to_epoch "$WDATE")            | Convert Date to epoch (WDATE='2021.01.4 20:04:53')    | 1609808693
| $(sadm_elapse "2016.01.30 10:00:4' '2016.01.30 10:00:03') | Elapse Time between two timestamps    | 00:00:41 |
| $(sadm_get_packagetype)                   | Get package type (rpm,deb,aix,dmg) of current host    | deb |
| $(sadm_server_type)                       | Host is Physical or Virtual (P/V)                     | P |
| $(sadm_server_model)                      | Server model (Ex: HP ProLiant DL580)                  | iMac12,2 | 
| $(sadm_server_serial)                     |  Server serial number (Ex: 4S7GYF1)                   |  Not |
| $(sadm_server_memory)                     | Server total memory in MB (Ex: 3790)                  | 11959 |
| $(sadm_server_hardware_bitmode)           | CPU Hardware capable of 32/64 bits                    | 64 |
| $(sadm_server_nb_logical_cpu)             | Number of Logical CPU on server                       | 4 |
| $(sadm_server_nb_cpu)                     | Number of Physical CPU on server                      | 1 |
| $(sadm_server_arch)                       | System Architecture                                   |x86_64 |
| $(sadm_server_nb_socket)                  | Number of socket on server                            |  1 |
| $(sadm_server_core_per_socket)            | Number of Core per Socket                             | 4 |
| $(sadm_server_thread_per_core)            | Number of Thread per Core                             | 1 |
| $(sadm_server_cpu_speed)                  | Server CPU Speed in MHz                               | 2093 |
| $(sadm_server_disks)                      | Disks list(MB) (DISKNAME\|SIZE,...)                   | sda\|1024000 |
| $(sadm_server_vg)                         | VG list(MB) (VGNAME\|SIZE\|USED\|FREE)                | rootvg\|476426\|466002\|10424 | 
| $(sadm_server_ips)                        | Net Dev (Name\|IP\|Netmask\|MAC)                      | eth0\|192.168.1.8\|255.255.255.0\|c8:2a:14:3b:59:a1 |
| $(sadm_tolower "Linux")                   | Return string in uppercase                            | LINUX |
| $(sadm_tolower "LINUX")                   | Return string in lowercase                            | linux | 
| $(sadm_capitalize "LINUX")                | Return 1st Char. in uppercase & rest in lower         | Linux |
| sadm_ask "Are you sure"                   | Display Question, wait Y/y(return 1) N/n(return 0)    | 1 |
| sadm_isnumeric 25                         | Return 0 if it is an integer else 1                   | 0 |
| sadm_check_requirements()                 | Check/Set Path of require commands                    | 0 or 1 |
| sadm_get_command_path "cmd"               | Get lscpu cmd path (return blank if not found)        | wlscpu=$(sadm_get_command_path "lscpu") |
| sadm_load_config_file                     | Load/Reload sadmin.cfg in Global Var.                 | Exit if fail |
| sadm_show_version                         | Show Script Name,Ver.,Libr.Ver,OS Name/Ver,KernelVer  | Used for script -v arg. |
| sadm_sleep 60 15                          | Sleep 60 seconds, update progress bar every 15 sec.   | 0...15...30...45...60 |
| [sadm_start]({% post_url 2019-10-12-sadmlib-std-demo-sh %}#sadm_start) | Init SADMIN Env. log, rch, tmpfile, pid | Exit if fail |
| [sadm_stop]({% post_url 2019-10-12-sadmlib-std-demo-sh %}#sadm_stop) 0 | Stop 0=Success 1=Error (Close log,rch Del PID,tmp) | 0 or 1 |
| sadm_trimfile "$file" 125                 | Trim file ($1) to number of lines ($2)                | sadm_trimfile "test.log" 125 |
| sadm_write "message"                      | Write message without LF in Log and Screen            | message  |
| sadm_writelog "message"                   | Write message with LF in Log and Screen               | message\n  |



{% include {{ site.section_environment }} %}

{% include {{ site.section_exitcode    }} %}

{% include {{ site.section_author      }} %}

{% include {{ site.section_copyright   }} %}


<a id="seealso"></a>
## SEE ALSO

[sadmlib_std.py ]({% post_url 2021-04-07-sadmlib-std-py %}) - SADMIN standard python library  
[sadmlib_screen.sh ]({% post_url 2019-10-12-sadmlib-screen-sh %}) - SADMIN screen oriented library  
[sadm_template.sh]({% post_url 2021-03-16-sadm-template-sh %}) - Using SADMIN Shell script template   
[sadm_template.py]({% post_url 2021-03-16-sadm-template-py %}) - Using SADMIN Python script template    
[sadm_template_menu.sh]({% post_url 2021-04-30-sadm-template-menu %}) - Using SADMIN shell menu template   
[sadmlib_std_demo.sh]({% post_url 2019-10-12-sadmlib-std-demo-sh %}) - SADMIN Shell Library Functions Demo   
[sadmlib_std_demo.py]({% post_url 2019-10-12-sadmlib-std-demo-py %}) - SADMIN Python Library Functions Demo  


