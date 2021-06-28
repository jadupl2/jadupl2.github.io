---
title:          hostname_sysinfo.txt
desc:           System information file
version:        3.24
summary: |         
  The **system information file ($SADMIN/dat/dr/$hostname_sysinfo.txt)** have two purposes :
  - It's used as an input file to the '[sadm_database_update.py]({% post_url 2021-05-29-sadm-database-update %})' 
    script to keep the server information up to date in the SADMIN database.
  - It also can be use in case of a disaster recovery to rebuild the server, along with all the other 
    files included in the disaster recovery directory ($SADMIN/dat/dr).
    {: .text-justify}
updated:        2021-06-02
os:             Linux, Aix, MacOS
type:           D  # [D]oc [S]=Server only [C]=Client [B]oth
layout:         single
search:         true
tags:           [ configuration_files ] 
categories:     [ configuration_files ] 
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
{{ page.summary }} 


<a id="name"></a>
## NAME
**{{ page.title }}** - *{{ page.desc }}*   
$SADMIN/dat/dr/$hostname_sysinfo.txt 

{% include sadm/sadm_page_info.md %}
{% if page.type == "S" %}
<font size="3"><strong>Can only be run on SADMIN Server.</strong></font>
{% endif %}
{% if page.type == "B" %}
<font size="3"><strong>Can be executed on a client and on the SADMIN Server.</strong></font>
{% endif %}




<a id="description"></a>
## DESCRIPTION

This text file is generated automatically every night on all clients by '[sadm_create_sysinfo.sh]({% post_url 2021-04-22-sadm-create-sysinfo %})', 
which is part of the "[sadm_client_sunset.sh]({% post_url 2021-05-31-sadm-client-sunset %})" script. 
The information contained in it, is used to update the server inventory information within the 
SADMIN database. This file contain key information about the server, the main IP address, the 
memory, the disks, the running O/S, it version, and all kind of useful information. You can also 
execute '[sadm_create_sysinfo.sh]({% post_url 2021-04-22-sadm-create-sysinfo %})' whenever you want, 
without problem.
{: .text-justify}

**Use the 'hostname_sysinfo.txt' file to update database**  
The script '[sadm_database_update.py]({% post_url 2021-05-29-sadm-database-update %})' read this 'sysinfo file' and update the appropriate server information in the SADMIN database.
information in the database. This update take place automatically early every morning on the SADMIN 
server. This script is executed as part of the '[sadm_server-sunrise.sh]({% post_url 2021-05-26-sadm-server-sunrise %})' script. You can also 
execute '[sadm_database_update.py]({% post_url 2021-05-29-sadm-database-update %})' whenever you want, without problem.
{: .text-justify}



<a id="examples"></a>
## EXAMPLE

```bash
# cat $SADMIN/dat/dr/rhel8_sysinfo.txt

# Nam of Cie - SysInfo Report File v3.24 - Wed Jun  2 23:24:58 EDT 2021
# # This file is use by 'sadm_database_update.py' to update the SADMIN database.
#                                                    
SADM_OS_TYPE                          = LINUX
SADM_UPDATE_DATE                      = 2021-06-02 23:24:58
SADM_HOSTNAME                         = rhel8
SADM_DOMAINNAME                       = maison.ca
SADM_HOST_IP                          = 192.168.1.5
SADM_SERVER_TYPE [V]irtual [P]hysical = V
SADM_OS_VERSION                       = 8.4
SADM_OS_MAJOR_VERSION                 = 8
SADM_OS_NAME                          = REDHAT
SADM_OS_CODE_NAME                     = Ootpa
SADM_KERNEL_VERSION                   = 4.18.0-305.el8.x86_64
SADM_KERNEL_BITMODE (32 or 64)        = 64
SADM_SERVER_MODEL                     = VIRTUALBOX
SADM_SERVER_SERIAL                    =  
SADM_SERVER_MEMORY (in MB)            = 1817
SADM_SERVER_HARDWARE_BITMODE          = 64
SADM_SERVER_NB_CPU                    = 1
SADM_SERVER_CPU_SPEED (in MHz)        = 2766
SADM_SERVER_ARCH                      = x86_64
SADM_SERVER_NB_SOCKET                 = 1
SADM_SERVER_CORE_PER_SOCKET           = 2
SADM_SERVER_THREAD_PER_CORE           = 1
SADM_SERVER_IPS                       = enp0s3|192.168.1.5|255.255.255.0|08:00:27:de:a5:0d
SADM_SERVER_DISKS (Size in MB)        = sda|27443
SADM_SERVER_VG(s) (Size in MB)        = rhel_rhel8|24576|19456|5120
SADM_OSUPDATE_DATE                    = 2021.05.31 05:30:27
SADM_OSUPDATE_STATUS                  = S
SADM_ROOT_DIRECTORY                   = /opt/sadmin
SADM_REAR_VERSION                     = 2.6
[root@rhel8 dr]# 
```
<!-- ![Daily Script Report Example](/assets/img/man/sadm_daily_report_script.png){: .align-center} -->

[Back to the top](#top_of_page)


<a id="seealso"></a>
## SEE ALSO

[sadmin.cfg]({% post_url 2021-04-26-sadmin-cfg %}) - SADMIN main configuration file   
[sadm_client_sunset.sh]({% post_url 2021-05-31-sadm-client-sunset %}) - Clients housekeeping and producing system information files  
[sadm_server-sunrise.sh]({% post_url 2021-05-26-sadm-server-sunrise %}) - Collect & process data produced by all actives clients  
[sadm_database_update.py]({% post_url 2021-05-29-sadm-database-update %}) - Take data collected from clients and update database    
[sadm_create_sysinfo.sh]({% post_url 2021-04-22-sadm-create-sysinfo %}) - Collect hardware & software information about the system  
