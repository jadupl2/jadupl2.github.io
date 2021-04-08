---
title:              sadmlib_std.sh
layout:             single
date_created:       2021-04-07
date_updated:       2021-04-08 
limit:              1
paginate:           false
show_excerpts:      false
entries_layout:     list
author_profile:     true
tags:               scripts
categories:         man 
toc:                false
classes:            wide
sadm_section_sh:    sadm/sadm_section_sh.md
---

Under construction, will be here soon.


## Explanation of the SADMIN section

### Global variable used by the SADMIN shell library
Available for you to use

| Variable Name |   Description | 
| :---  | :--- | 
| SADM_PN=${0##*/}                                 |  Current Script filename(with extension)|   
| SADM_INST=`echo "$SADM_PN" |cut -d'.' -f1`       | Current Script filename(without extension)|   
| SADM_TPID="$$"                                   |  Current Script Process ID.|   
| SADM_HOSTNAME=`hostname -s`                      |  Current Host name without Domain Name|   
| SADM_OS_TYPE=`uname -s | tr '[:lower:]' '[:upper:]'` |  Operating System Type in uppercase LINUX,AIX,DARWIN,SUNOS |   

<br>

---

### Global variables you can change and that affect library behavior

| Variable Name |   Description |  Example of return value | 
| :---  | :--- | :---  |
| $SADM_VER                    | Your script Version Number               | 3.20                  |         
| $SADM_PN                     | Script Name                         | sadmlib_std_demo.sh   |         
| $SADM_INST                   | Script Name Without Extension       | sadmlib_std_demo      |         
| $SADM_USERNAME               | Contain the current user name                   | root                  |         
| $SADM_TPID                   | Current Process ID                  | 27933                 |         
| $SADM_MULTIPLE_EXEC          | Allow running multiple copy [Y/N]   | Y                     |         
| $SADM_USE_RCH                | Generate entry in '*.rch' file      | N                     |         
| $SADM_LOG_TYPE               | Set Output to [S]creen [L]og [B]oth | B                     |         
| $SADM_LOG_APPEND             | Append to Log=Y, Create new log=N   | N                     |         
| $SADM_LOG_HEADER             | Generate Header in log [Y,N]        | N                     |         
| $SADM_LOG_FOOTER             | Generate or not Footer in log [Y/N] | N                     |         
| $SADM_EXIT_CODE              | Current value of script exit code   | 0                     |         

<br>

---

## SADMIN Standard library functions

| Function Call |   Description |  Return value example | 
| :---  | :--- | :---  |
| $(sadm_get_release)                       | Return the SADMIN Release Number (XX.XX)       | 1.2.9 |
| $(sadm_get_ostype)                        | Return the OS type in uppercase (LINUX,AIX,DARWIN) |  LINUX |
| $(sadm_get_osversion)                   | Return the O/S version (Ex: 7.2, 6.5)   | 7.9.2009 |
| $(sadm_get_osmajorversion)          | Return the O/S major version (Ex 7, 6)  |  7 |
| $(sadm_get_osminorversion)          | Return the O/S minor version (Ex 2, 3)  |  9  |
| $(sadm_get_osname)                       | Return the O/S name in uppercase (REDHAT,CENTOS,UBUNTU,...) |  CENTOS |
| $(sadm_get_oscodename)               | Return the O/S project code name               | focal |
| $(sadm_get_kernel_version)             | Return the O/S kernel version          | 5.4.0-58-generic |
| $(sadm_get_kernel_bitmode)           | Return the O/S kernel bit mode (32 or 64)      |  64 |
| $(sadm_get_hostname)                    | Return the current host name                   | imac |
| $(sadm_get_host_ip)                         | Return the current host IP address             | 192.168.1.8 |
| $(sadm_get_domainname)               | Return the current host domain name            | maison.ca |
| $(sadm_get_fqdn)                               | Return fully qualified domain host name    | imac.maison.ca |
| $(sadm_get_epoch_time)                  | Return the current epoch time                     | 1609808693 |
| $(sadm_epoch_to_date 1609808693) | Convert epoch time to date          | 2021.01.4 20:04:53 |
| $(sadm_date_to_epoch "$WDATE")  | Convert Date to epoch time (WDATE='2021.01.4 20:04:53')         | 1609808693
| $(sadm_elapse "2016.01.30 10:00:4' '2016.01.30 10:00:03') | Elapse Time between two timestamps | 00:00:41 |
| $(sadm_get_packagetype)         | Get package type (rpm,deb,aix,dmg) of current host  | deb |
| $(sadm_server_type)                   | Host is Physical or Virtual (P/V)   | P |
| $(sadm_server_model)                       | Server model (Ex: HP ProLiant DL580)     |  iMac12,2 | 
| $(sadm_server_serial)                         |  Server serial number (Ex: 4S7GYF1)        |  Not |
| $(sadm_server_memory)                     | Server total memory in MB (Ex: 3790)          | 11959 |
| $(sadm_server_hardware_bitmode)  | CPU Hardware capable of 32/64 bits             | 64 |
| $(sadm_server_nb_logical_cpu)         | Number of Logical CPU on server                | 4 |
| $(sadm_server_nb_cpu)                      | Number of Physical CPU on server             | 1 |
| $(sadm_server_arch)                            | System Architecture                              |x86_64 |
| $(sadm_server_nb_socket)                  | Number of socket on server                     |  1 |
| $(sadm_server_core_per_socket)        | Number of Core per Socket                  | 4 |
| $(sadm_server_thread_per_core)     | Number of Thread per Core                        | 1 |
| $(sadm_server_cpu_speed)               | Server CPU Speed in MHz                      | 2093 |
| $(sadm_server_disks)                      | Disks list(MB) (DISKNAME\|SIZE,...)       | sda\|1024000 |
| $(sadm_server_vg)                          | VG list(MB) (VGNAME|SIZE|USED|FREE) | | 
| $(sadm_server_ips)                        | Network IP(Name|IP|Netmask|MAC)       | enp2s0\|192.168.1.8\|255.255.255.0\|c8:2a:14:3b:59:a1 |
| $(sadm_tolower "Linux")                      | Return string in uppercase                           |  LINUX |
| $(sadm_tolower "LINUX")                  | Return string in lowercase                               | linux | 
| $(sadm_capitalize "LINUX")               | Return string capitalize  (1st Char. in uppercase & rest in lower)                            |  Linux |
| sadm_isnumeric() |  | |
| sadm_check_requirements() |  | |
| sadm_get_command_path() |  | |
| sadm_get_host_ip() |  | |
| sadm_get_packagetype() |  | |
| $(sadm_get_release)              | Return SADMIN release number (XX.XX)       |  1.2.9 |
| sadm_isnumeric() |  | |
| sadm_load_config_file() |  | |
| sadm_send_alert() |  | |
| sadm_server_arch() |  | |
| sadm_server_disks() |  | |
| sadm_server_ips() |  | |
| sadm_server_type() |  | |
| sadm_server_vg() |  | |
| sadm_show_version() |  | |
| sadm_start() |  | |
| sadm_stop() |  | |
| sadm_trimfile() |  | |
| sadm_writelog() |  | |
| write_alert_history() |  | |

