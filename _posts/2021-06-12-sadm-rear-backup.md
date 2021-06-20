---
title:          sadm_rear_backup.sh
desc:           Perform a Rear image backup to a NFS server, ready for a disaster recovery
version:        2.28
summary: |         
    This script create an image backup that can be later use to recover your whole system in case of a disk crash.
    [Relax-and-Recover(ReaR)](https://relax-and-recover.org/) is a recovery and system migration utility.
    {: .text-justify}
updated:        2021-06-17
os:             Linux
type:           B  # [D]oc [S]=Server only [C]=Client [B]oth
categories:     [ backup ] 
tags:           [ backup ] 
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
**{{ page.title }}**  
*{{ page.desc }}*   



<a id="synopsis"></a>
## SYNOPSIS

```bash
{{ page.title }} [-d 0-9] [-h] [-v] [-n]
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

{{ page.summary }} 

The script produces a bootable image (.iso) and a backup (.tgz) file.
It allows to restore to different hardware and can therefore be used as a migration utility as well.

### Destination of the ReaR backup

Destination of the ReaR backup is defined in the [SADMIN configuration file ($SADMIN/cfg/sadmin.cfg)]({% post_url 2021-04-26-sadmin-cfg %}#sadm_rear_nfs_server).
Below is a portion of the 'sadmin.cfg' dedicated to the ReaR backup.

![ReaR Backup Destination](/assets/img/sadm_rear_backup/sadm_rear_backup_dest.png){: .align-center}



### SADMIN ReaR configuration file (/etc/rear/site.conf)

[ReaR](https://relax-and-recover.org/) configuration files are located in /etc/rear directory.
The files /etc/rear/os.conf & /etc/rear/local.conf, should not be modified as they can overwritten by future version of the ReaR package.
All your changes (if any), should be done to '/etc/rear/site.conf', this file won't be touch by any future update.
The variable "$HOSTNAME" will be replace by the hostname at execution time, along with the "BACKUP_URL" variable that will be replace by the value you have define in the SADMIN configuration file.

![ReaR Config File](/assets/img/sadm_rear_backup/sadm_rear_site_conf.png){: .align-center}

<a id="rear_schedule"></a>
### Scheduling a ReaR backup 

You can run the ReaR backup just by typing 'sadm_rear_backup.sh' at the command line. It is 
recommended to use the web interface and scheduled the ReaR backup to run automatically on a 
regular basis. To schedule a ReaR image backup using the SADMIN web interface, click on 
“ReaR Backup” in the heading portion of the web interface. 
{: .text-justify}

![ReaR heading link](/assets/img/sadm_rear_backup/sadm_rear_heading.png){: .align-center}

Then click on the server name you want to schedule.
![ReaR choose server](/assets/img/sadm_rear_backup/sadm_rear_server.png){: .align-center}

- To activate the ReaR backup via the web interface, you must 'Activate ReaR Backup' and remember that the status of the system must be active.  
- The chosen schedule will get propagated in the '/etc/cron.d/sadm_rear_backup' cron file shortly after that (at the next run of '[sadm_fetch_client.sh]({% post_url 2021-03-16-sadm-fetch-client %})'.  
- Unless you want to exclude some filesystem, volume group you can leave the text box like it is.

![ReaR Web Interface](/assets/img/sadm_rear_backup/sadm_rear_backup_web.png){: .align-center}

I will document the restore process of a ReaR backup later on, but frankly it is quite easy. So far
I have done a few backup/restore and it went well.

[Back to the top](#top_of_page)



<a id="examples"></a>
## EXAMPLE

```bash
[rhel8]# sadm_rear_backup.sh 

================================================================================
Tue Jun 15 01:00:39 EDT 2021 - sadm_rear_backup.sh V2.28 - SADM Lib. V3.70
Server Name: rhel8.maison.ca - Type: LINUX
REDHAT 8.4 Kernel 4.18.0-305.3.1.el8_4.x86_64
==================================================

STARTING ReaR PREPARATIONs
Update backup destination in /etc/rear/site.conf with value from sadmin.cfg.
  - BACKUP_URL="nfs://batnas.maison.ca/volume1/backup_rear"
  - Update actual /etc/rear/site.conf [ OK ]
Create local temporary mount point directory (/mnt/rear_273600).
Mount the NFS share on batnas.maison.ca system.
mount batnas.maison.ca:/volume1/backup_rear /mnt/rear_273600 [ OK ]
batnas.maison.ca:/volume1/backup_rear  5.5T  4.6T  865G  85 /mnt/rear_273600
Write test to NFS mount ... [ OK ]

Rename previous ISO rear_rhel8.iso to rear_rhel8_2021-06-08_01:05:37.iso [ OK ]
Rename previous backup rear_rhel8.tar.gz to rear_rhel8_2021-06-08_01:17:15.tar.gz[ OK ]
END OF ReaR PREPARATION [ SUCCESS ]
==================================================

CREATING THE 'ReaR' BACKUP
/usr/sbin/rear mkbackup -v
Relax-and-Recover 2.6 / 2020-06-17
Running rear mkbackup (PID 288159)
Using log file: /var/log/rear/rear-rhel8.log
Running workflow mkbackup on the normal/original system
Using backup archive '/tmp/rear.yc8NGAFLYZdeTJy/outputfs/rhel8/rear_rhel8.tar.gz'
Using autodetected kernel '/boot/vmlinuz-4.18.0-305.3.1.el8_4.x86_64' as kernel in the recovery system
Creating disk layout
Overwriting existing disk layout file /var/lib/rear/layout/disklayout.conf
Using guessed bootloader 'GRUB' (found in first bytes on /dev/sda)
Verifying that the entries in /var/lib/rear/layout/disklayout.conf are correct ...
Creating recovery system root filesystem skeleton layout
Skipping 'virbr0': not bound to any physical interface.
Copying logfile /var/log/rear/rear-rhel8.log into initramfs as '/tmp/rear-rhel8-partial-2021-06-15T01:00:50-04:00.log'
Copying files and directories
Copying binaries and libraries
Copying all kernel modules in /lib/modules/4.18.0-305.3.1.el8_4.x86_64 (MODULES contains 'all_modules')
Copying all files in /lib*/firmware/
Testing that the recovery system in /tmp/rear.yc8NGAFLYZdeTJy/rootfs contains a usable system
Creating recovery/rescue system initramfs/initrd initrd.cgz with gzip default compression
Created initrd.cgz with gzip default compression (384808064 bytes) in 67 seconds
Making ISO image
Wrote ISO image: /var/lib/rear/output/rear_rhel8.iso (379M)
Copying resulting files to nfs location
Saving /var/log/rear/rear-rhel8.log as rear-rhel8.log to nfs location
Making backup (using backup method NETFS)
Creating tar archive '/tmp/rear.yc8NGAFLYZdeTJy/outputfs/rhel8/rear_rhel8.tar.gz'
Preparing archive operationOK
Archived 3143 MiB in 703 seconds [avg 4579 KiB/sec]
Exiting rear mkbackup (PID 288159) and its descendant processes ...
Running exit tasks
ReaR backup exit code : 0
More info in the log /opt/sadmin/log/rhel8_sadm_rear_backup.log.
Rear Backup completed [ SUCCESS ]
==================================================
Perform ReaR housekeeping.
Information coming from /opt/sadmin/cfg/sadmin.cfg:
 - Always keep last 3 backup on 'batnas.maison.ca'
List of ReaR backup and ISO actually on NFS Server for rhel8
-rw-rw-r-- 1 jacques users 378M May 25 01:04 /mnt/rear_273600/rhel8/rear_rhel8_2021-05-25_01:04:51.iso
-rw-rw-r-- 1 jacques users 2.8G May 25 01:15 /mnt/rear_273600/rhel8/rear_rhel8_2021-05-25_01:15:57.tar.gz
-rw-rw-r-- 1 jacques users 378M Jun  1 01:05 /mnt/rear_273600/rhel8/rear_rhel8_2021-06-01_01:05:05.iso
-rw-rw-r-- 1 jacques users 2.8G Jun  1 01:16 /mnt/rear_273600/rhel8/rear_rhel8_2021-06-01_01:16:07.tar.gz
-rw-rw-r-- 1 jacques users 378M Jun  8 01:05 /mnt/rear_273600/rhel8/rear_rhel8_2021-06-08_01:05:37.iso
-rw-rw-r-- 1 jacques users 3.1G Jun  8 01:17 /mnt/rear_273600/rhel8/rear_rhel8_2021-06-08_01:17:15.tar.gz
-rw------- 1 nobody  users 379M Jun 15 01:05 /mnt/rear_273600/rhel8/rear_rhel8.iso
-rw------- 1 nobody  users 3.1G Jun 15 01:17 /mnt/rear_273600/rhel8/rear_rhel8.tar.gz
-rw-rw-r-- 1 jacques users  15M Jun 15 01:17 /mnt/rear_273600/rhel8/rear_rhel8.log

Number of backup file(s) to delete is 1
Backup file(s) that will be Deleted :
/mnt/rear_273600/rhel8/rear_rhel8_2021-05-25_01:15:57.tar.gz
Backup deleted [ OK ]

Number of ISO file(s) to delete is 1
Backup ISO file(s) that will be Deleted :
/mnt/rear_273600/rhel8/rear_rhel8_2021-05-25_01:04:51.iso
ISO deleted [ OK ]

Content of rhel8 ReaR backup directory after housekeeping.
-rw-rw-r-- 1 jacques users 378M Jun  1 01:05 /mnt/rear_273600/rhel8/rear_rhel8_2021-06-01_01:05:05.iso
-rw-rw-r-- 1 jacques users 2.8G Jun  1 01:16 /mnt/rear_273600/rhel8/rear_rhel8_2021-06-01_01:16:07.tar.gz
-rw-rw-r-- 1 jacques users 378M Jun  8 01:05 /mnt/rear_273600/rhel8/rear_rhel8_2021-06-08_01:05:37.iso
-rw-rw-r-- 1 jacques users 3.1G Jun  8 01:17 /mnt/rear_273600/rhel8/rear_rhel8_2021-06-08_01:17:15.tar.gz
-rw------- 1 nobody  users 379M Jun 15 01:05 /mnt/rear_273600/rhel8/rear_rhel8.iso
-rw------- 1 nobody  users 3.1G Jun 15 01:17 /mnt/rear_273600/rhel8/rear_rhel8.tar.gz
-rw-rw-r-- 1 jacques users  15M Jun 15 01:17 /mnt/rear_273600/rhel8/rear_rhel8.log

Unmounting NFS mount directory /mnt/rear_273600 ...
umount /mnt/rear_273600 [ OK ]
ReaR Backup Housekeeping [ SUCCESS ]
==================================================
Script exit code is 0 (Success) and execution time is 00:17:19
History (/opt/sadmin/dat/rch/rhel8_sadm_rear_backup.rch) trim to 35 lines.
Script will send an alert only when it terminate with error ($SADM_ALERT_TYPE=1).
Script succeeded, no alert will be send to 'default' alert group.
New log (/opt/sadmin/log/rhel8_sadm_rear_backup.log) created ($SADM_LOG_APPEND='N').
End of sadm_rear_backup.sh - Tue Jun 15 01:17:24 EDT 2021
================================================================================
[rhel8]# 
```

[Back to the top](#top_of_page)


{% include {{ site.section_options     }} %}
| **-n** | Do not compress backup file(s) | 
    
{% include {{ site.section_environment }} %}

{% include {{ site.section_exitcode    }} %}

{% include {{ site.section_author      }} %}

{% include {{ site.section_copyright   }} %}


<a id="seealso"></a>
## SEE ALSO

| Link to ...| Description |  
| :--- | :--- |  
| [sadm_daily_report]({% post_url 2021-04-01-sadm-daily-report %})                  | Produce and email monitoring daily reports
| [How-to Add a client]({% post_url 2021-04-11-web-add-client %})                   | How-to add a client to SADMIN inventory  
| [sadm_backup.sh]({% post_url 2021-05-24-sadm-backup %})                           | Backup based on the content of the backup list & exclude file  
| [sadmin.cfg]({% post_url 2021-04-26-sadmin-cfg %})                                | SADMIN main configuration file   
| [sadm_backupdb.sh]({% post_url 2021-05-26-sadm-backupdb %})                       | Backup one or all MySQL/MariaDB databases on the system  
