---
title:          sadm_dr_savefs.sh
desc:           Save system filesystems information in order to recreate them from scratch
version:        2.8
updated:        2021-06-02
os:             Linux
type:           B  # [D]oc [S]=Server only [C]=Client [B]oth
categories:     [ client-scripts ] 
tags:           [ client-scripts ] 
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

UNDER CONSTRUCTION ******

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

This script save filesystem information in order to recreate them from scratch.
It is run daily by the 'sadm_client_sunset.sh' script.
The output file is use to recreate all the system filesystem in a disaster recovery situation.
This script is supported on Aix and Linux.
Although it run on MacOS, it doesn't produce anything (No lvm on MacOS).

On Linux :

    The Volume Group(s) where the filesystems will be recreated, must be created prior to running this script.
    If the 'lvm2' package is not installed (lvm not used), the script inform the user and exit the script
    The 'lvscan' command output is used and each logical volume is process one by one.
    It gather all info needed to recreate the filesystem (or swap) needed in case of disaster recovery.
    The output file name "$SADMIN/dat/dr/[hostname]_fs_save_info.dat" is created with all info needed to recreate filesystems
    Output file is sorted in order of mount point length (So that /abc if created before /abc/123).
    It is use by "sadm_dr_recreatefs.sh" script to recreate all filesystems of the specified VG, with the proper permission.

Output when running the script


        $ sadm_dr_savefs.sh 
        ================================================================================
        Starting sadm_dr_savefs.sh V2.7 - SADM Lib. V2.52
        Server Name: holmes.maison.ca - Type: LINUX
        CENTOS 7.6.1810 Kernel 3.10.0-957.1.3.el7.x86_64
        ==================================================
        
        Verifying if 'lvm2' package is installed ...
        [OK] lvm2 package is installed ...
        There are 21 Logical volume reported by lvscan
        Output file is /sadmin/dat/dr/holmes_fs_save_info.dat
        
        Backup of /sadmin/dat/dr/holmes_fs_save_info.dat to /sadmin/dat/dr/holmes_fs_save_info.prev
        Creating a new copy of /sadmin/dat/dr/holmes_fs_save_info.dat
        [SUCCESS] Copying /sadmin/dat/dr/holmes_fstab to /sadmin/dat/dr/holmes_fstab.prev
        [SUCCESS] Copying /etc/fstab to /sadmin/dat/dr/holmes_fstab
        
        ==================================================
        Script return code is 0
        Script execution time is 00:00:04
        Trim History /sadmin/dat/rch/holmes_sadm_dr_savefs.rch to 125 lines
        Requested alert only if script fail (Won't send alert)
        Trim log /sadmin/log/holmes_sadm_dr_savefs.log to 2000 lines
        Fri Dec  7 11:03:12 EST 2018 - End of sadm_dr_savefs.sh
        ================================================================================
        $ 
        



Example of the file produced :


        root@holmes:/sadmin/bin$ cat /sadmin/dat/dr/holmes_fs_save_info.dat
        # SADMIN - Filesystem Info. for system holmes.maison.ca
        # File was created by sadm_dr_savefs.sh on Tue Nov 20 14:00:30 EST 2018
        # This file is use in a Disaster Recovery situation
        # The data below is use by sadm_dr_recreatefs.sh to recreate filesystems
        # ---------------------------------------------------------------------
        # 
        rootvg::swap00:swap:3072:::0000
        rootvg::swap01:swap:4096:::0000
        rootvg:/:root:xfs:2048:root:root:0555
        rootvg:/opt:opt:xfs:2048:root:root:0755
        rootvg:/tmp:tmp:xfs:3072:root:root:1777
        rootvg:/usr:usr:xfs:12001:root:root:0755
        rootvg:/var:var:xfs:4997:root:root:0755
        rootvg:/coco:cocolv:xfs:404:root:root:0755
        rootvg:/home:home:xfs:12001:root:root:0755
        rootvg:/wiki:wikilv:xfs:4096:apache:apache:2775
        rootvg:/sadmin:sadmin:xfs:4096:sadmin:sadmin:0775
        rootvg:/storix:storix:xfs:768:root:root:0775
        rootvg:/backups:backlv73:xfs:2048:sadmin:jacques:2775
        rootvg:/install:install:ext4:59996:sadmin:jacques:0775
        rootvg:/mystuff:vault:xfs:4096:sadmin:jacques:2775
        rootvg:/psadmin:psadminlv:xfs:2048:sadmin:sadmin:0775
        rootvg:/wsadmin:tadminlv:xfs:2048:apache:jacques:2775
        rootvg:/archives:lvx:xfs:249999:staff:jacques:2777
        rootvg:/gitrepos:gitlv:ext4:4096:git:git:2775
        rootvg:/sysadmin:sysadm:xfs:128:sadmin:jacques:0775
        rootvg:/linternux:linternux:xfs:4096:apache:apache:2775
        


On Aix :

    This script doesn't save any information about the 'rootvg' volume group, we assume that it will be restore by the 'mksysb'.
    Files produced are meant to be use by sadm_dr_recreatefs.sh to recreate the volume group and the filesystems it contain.
    It produce two files, this first is named $SADMIN/dat/dr/HOSTNAME_pvinfo.txt
        In the output file, we have a list of all physical volumes with the name of the VG they belong
        Along with that, we have disk space used by each VG and then the size of each physical volume.


                        hdisk0          000549ca5ae0508d                    rootvg          active      
                        hdisk1          000549ca5afe98bd                    None                        
                        hdisk2          0004d08c89dd230c                    nimvg           active      
                        Used space for nimvg: (15616 megabytes)     <<-------- Used space in 'nimvg'
                        hdisk0:140013                               <<-------- Size of hdisk0
                        hdisk1:140013                               <<-------- Size of hdisk1
                        hdisk2:140013                               <<-------- Size of hdisk2
                        

        By looking at the information above, we can say that the volume group 'nimvg' need a dedicated disk (or group of disk) with at least 15GB of free space to be restore.

    The second file is a backup of the structure of each volume group (except 'rootvg').
        The backup file is in backup/restore format and is created in $SADMIN/dat/dr directory.
        In the example below, the file was created on a server named 'aixb50', it contain the metadata of the volume group 'datavg' and have an extension of '.savevg'
        It is worth mentionning that raw devices are included in the backup and will be restore by the sadm_dr_recreatefs.sh script.


                    root@aixb50(/sadmin/dat/dr)# file aixb50_datavg.savevg
                    aixb50_datavg.savevg: backup/restore format file
                    root@aixb50(/sadmin/dat/dr)#
                    

        Both of the files created are quite small, since no users files is included in the backup, only the metadata.


                    root@holmes:/sadmin/dat/dr$ ls -l batman_nimvg.savevg batman_pvinfo.txt
                    -rwxrwxr-x 1 apache apache 51200 Oct 29 11:30 batman_nimvg.savevg
                    -rwxrwxr-x 1 apache apache   325 Oct 29 11:30 batman_pvinfo.txt
                    root@holmes:/sadmin/www/dat/batman/dr$ 
                    

    The script make sure that an exclude file (/etc/exclude.VGNAME) exist for each VG and that it contain this line ".*".
        This ensure that no file is taken in the backup of the VG (Only the structure metadata).
        These exclude file will be delete at the end of the backup.
        When the backup of a VG is done the line that was added in the exclude file is removed.


 
{: .text-justify}
 
```bash
# include script
```

[Back to the top](#top_of_page)



<a id="examples"></a>
## EXAMPLE

```bash
# Example of script output
```
<!-- ![Daily Script Report Example](/assets/img/man/sadm_daily_report_script.png){: .align-center} -->

[Back to the top](#top_of_page)


{% include {{ site.section_options     }} %}
| **-i** | option -i | 

{% include {{ site.section_environment }} %}

{% include {{ site.section_exitcode    }} %}

{% include {{ site.section_author      }} %}

{% include {{ site.section_copyright   }} %}


<a id="seealso"></a>
## SEE ALSO

[sadm_fetch_client.sh]({% post_url 2021-03-16-sadm-fetch-client %}) - rsync all .rch/.log/.rpt from actives clients to the SADMIN server.  
[sadm_requirements.sh]({% post_url 2019-03-21-sadm-requirements %}) - List/install required SADMIN tools packages  
[sadm_sysmon_tui.pl]({% post_url 2021-05-18-sadm-sysmon-tui %}) -  Command line summary of alerts and failed scripts of all your servers.  
[sadm_daily_report]({% post_url 2021-04-01-sadm-daily-report %}) - Produce and email monitoring daily reports
[sadm_template.sh]({% post_url 2021-03-16-sadm-template-sh %}) - Using SADMIN shell script template   
[sadm_template.py]({% post_url 2021-03-16-sadm-template-py %}) - Using SADMIN python script template    
[sadm_template_menu.sh]({% post_url 2021-04-30-sadm-template-menu %}) - Using SADMIN shell menu template   
[sadm_wrapper.sh]({% post_url 2018-02-11-sadm-wrapper %}) - Use to run your existing scripts & benefit of SADMIN tools  
[sadmlib_std.sh]({% post_url 2021-04-07-sadmlib-std-sh %}) - SADMIN standard shell library  
[sadmlib_std.py]({% post_url 2021-04-07-sadmlib-std-py %}) - SADMIN standard python library  
[sadmlib_screen.sh]({% post_url 2019-10-12-sadmlib-screen-sh %}) - SADMIN screen oriented library  
[sadmlib_std_demo.sh]({% post_url 2019-10-12-sadmlib-std-demo-sh %}) - SADMIN shell library functions demo   
[sadmlib_std_demo.py]({% post_url 2019-10-12-sadmlib-std-demo-py %}) - SADMIN python library functions demo  
[SADMIN installation](/_pages/install) - SADMIN installation page  
[How-to Add a client]({% post_url 2021-04-11-web-add-client %}) - How-to add a client to SADMIN inventory  
[How-to Remove a client]({% post_url 2021-05-19-how-to-remove-a-client %}) - How-to remove a client from SADMIN inventory  
[sadm_uninstall.sh]({% post_url 2021-05-21-sadm-uninstall %}) - Uninstall the SADMIN tools  
[sadm_push_sadmin.sh]({% post_url 2021-05-22-sadm-push-sadmin %}) - Push SADMIN version to one or all actives clients  
[How-to update SADMIN]({% post_url 2021-03-14-sadm-update %}) - How-to update to latest version of SADMIN   
[sadm_service_ctrl.sh]({% post_url 2021-05-23-sadm-service-ctrl %}) - Enable, Disable and get status of system startup and shutdown script  
[sadm_backup.sh]({% post_url 2021-05-24-sadm-backup %}) - Backup based on the content of the backup list & exclude file  
[sadmin.cfg]({% post_url 2021-04-26-sadmin-cfg %}) - SADMIN main configuration file   
[sadm_server-sunrise.sh]({% post_url 2021-05-26-sadm-server-sunrise %}) - Collect & process data produced by all actives clients  
[sadm_server_housekeeping.sh]({% post_url 2021-05-27-sadm-server-housekeeping %}) - Enforce security SADMIN Web interface & crontab files
[sadm_daily_farm_fetch.sh]({% post_url 2021-05-28-sadm-daily-farm-fetch %}) - Collect Hardware/Software/Performance data from actives servers   
[sadm_database_update.py]({% post_url 2021-05-29-sadm-database-update %}) - Take data collected from clients and update database    
[sadm_nmon_rrd_update.sh]({% post_url 2021-05-29-sadm-nmon-rrd-update %}) - Daily performance database update   
[sadm_subnet-lookup.py]({% post_url 2021-05-29-sadm-subnet-lookup %}) - Scan network selected subnet & store info in database  
[sadm_backupdb.sh]({% post_url 2021-05-26-sadm-backupdb %}) - Backup one or all MySQL/MariaDB databases on the system  
[sadm_client_sunset.sh]({% post_url 2021-05-31-sadm-client-sunset %}) - Clients end of day housekeeping and producing system information files  
[sadm_client_housekeeping.sh]({% post_url 2021-05-29-sadm-client-housekeeping %}) - Purge old log,rch,nmon files and check $SADMIN permission   
[sadm_create_sysinfo.sh]({% post_url 2021-04-22-sadm-create-sysinfo %}) - Collect hardware & software information about the system   
[System Information File]({% post_url 2021-05-30-sysinfo-file %}) - Documentation about the system information file  

