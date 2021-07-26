---
title:          sadm_database_update.py
desc:           Take system information collected files from clients and update database
version:        3.13
updated:        2021-06-03
os:             Linux
type:           S  # [D]oc [S]=Server only [C]=Client [B]oth
tags:           [ server-scripts ] 
categories:     [ server-scripts ] 
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


<a id="name"></a>
## NAME
**{{ page.title }}**  
*{{ page.desc }}*   



<a id="synopsis"></a>
## SYNOPSIS

```bash
{{ page.title }} [-d 0-9] [-h] [-v]
```
{% include sadm/sadm_page_info.md %}
{% if page.type == "S" %}
<font size="3"><strong>Can only be run on SADMIN Server.</strong></font>
{% endif %}
{% if page.type == "B" %}
<font size="3"><strong>Can be executed on a client and on the SADMIN Server.</strong></font>
{% endif %}




<a id="description"></a>
## DESCRIPTION
The function of this script is to read the [system information file]({% post_url 2021-05-30-sysinfo-file %}) 
that was produced by each client
and to update the corresponding system in SADMIN database. This script is run automatically every 
morning by the [sadm_server-sunrise.sh]({% post_url 2021-05-26-sadm-server-sunrise %}) script.
{: .text-justify}
 
[Back to the top](#top_of_page)



<a id="examples"></a>
## EXAMPLE

```bash
# sadm_database_update.py 
================================================================================
Starting sadm_database_update.py V3.12 - SADM Lib. V3.18
Server Name: holmes.maison.ca - Type: Linux
O/S: Centos  7.9.2009 - Code Name: Core
==================================================
 
Processing all actives systems

----------------------------------------
Processing (1) borg.maison.ca  - os:ubuntu
Reading sysinfo file : /sadmin/www/dat/borg/dr/borg_sysinfo.txt
Updating borg.maison.ca data in Database
[OK] borg update Succeeded

----------------------------------------
Processing (2) centos6.maison.ca - os:centos
Reading sysinfo file : /sadmin/www/dat/centos6/dr/centos6_sysinfo.txt
Updating centos6.maison.ca data in Database
[OK] centos6 update Succeeded
...
...
---------------------------------------
Processing (10) imac.maison.ca  - os:macosx
Reading sysinfo file : /sadmin/www/dat/imac/dr/imac_sysinfo.txt
Updating imac.maison.ca data in Database
[OK] imac update Succeeded
...
...
----------------------------------------
Processing (25) yoda.maison.ca  - os:fedora
Reading sysinfo file : /sadmin/www/dat/yoda/dr/yoda_sysinfo.txt
Updating yoda.maison.ca data in Database
[OK] yoda update Succeeded
 
==================================================
Script return code: 0
Script execution time is 00:00:02
Trim /sadmin/dat/rch/holmes_sadm_database_update.rch to 35 lines.
Alert requested if script fail.
Trim /sadmin/log/holmes_sadm_database_update.log to 500 lines.
Sun May 30 11:45:43 2021 - End of sadm_database_update.py
================================================================================
```
<!-- ![Daily Script Report Example](/assets/img/man/sadm_daily_report_script.png){: .align-center} -->

[Back to the top](#top_of_page)


{% include {{ site.section_options     }} %}

{% include {{ site.section_environment }} %}

{% include {{ site.section_exitcode    }} %}

{% include {{ site.section_author      }} %}

{% include {{ site.section_copyright   }} %}


<a id="seealso"></a>
## SEE ALSO

[sadm_server-sunrise.sh]({% post_url 2021-05-26-sadm-server-sunrise %}) - Collect & process data produced by all actives clients  
[sadm_server_housekeeping.sh]({% post_url 2021-05-27-sadm-server-housekeeping %}) - Purge old log,rch,nmon files and check $SADMIN permission   
[sadm_daily_farm_fetch.sh]({% post_url 2021-05-28-sadm-daily-farm-fetch %}) - Collect Hardware/Software/Performance data from actives servers   
[sadm_fetch_clients.sh]({% post_url 2021-03-16-sadm-fetch-clients %}) - rsync all .rch/.log/.rpt from actives clients to the SADMIN server.  
[sadm_create_sysinfo.sh]({% post_url 2021-04-22-sadm-create-sysinfo %}) - Collect hardware & software information about the system  
[sadmin.cfg]({% post_url 2021-04-26-sadmin-cfg %}) - SADMIN main configuration file   
