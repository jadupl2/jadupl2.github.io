---
title:          sadm_dr_recreatefs.sh
desc:           Used metadata saved by 'sadm_dr_savefs.sh' to recreate host filesystems
version:        2.3
updated:        2021-06-04
os:             Linux, Aix
type:           C  # [D]oc [S]=Server only [C]=Client [B]oth
categories:     [ utilities ] 
tags:           [ utilities ] 
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

**Linux - Recreating the filesystems and populate /etc/inittab**  

I use to work at a company where we use lvm a lot (Logical Volume Manager), every disk added to a system
was assigned a lvm partition. It was easy to add new disks to an existing (or new) volume
group. We would then enlarge the filesystems that needed space and we were done. We could all do that
online without downtime or disruption. If you are using the LVM in a similar fashion then this 
utility could be interesting for you. If you've lost completely your server content, then with script
you would be able to recreate all the filesystems that you had before the crash with the right 
size, permission and ownership (owner/group), ready to begin the restore of your data. If this 
seem interesting for you read on. 
{: .text-justify}

- Every day the '[sadm_dr_savefs.sh]({% post_url 2021-06-02-sadm-dr-savefs %})' script run and generate 
one output file name "$SADMIN/dat/dr/[hostname]_fs_save_info.dat".  
- The '[sadm_dr_savefs.sh]({% post_url 2021-06-02-sadm-dr-savefs %})' script is part of the 
'[sadm_client_sunset.sh]({% post_url 2021-05-31-sadm-client-sunset %})' that is scheduled to run 
daily from the client crontab (/etc/cron.d/sadm_client).
- The output file of '[sadm_dr_savefs.sh]({% post_url 2021-06-02-sadm-dr-savefs %})' become the input file of this script.  

In our example, we will use the file that was produced on a system name "gotham", so the file name is "$SADMIN/dat/dr/gotham_fs_save_info.dat".
This file is use to recreate all filesystems of the specified volume group.
The recreated filesystems will have the same permission, owner and group as on the original server.
This script will not recreate the user or the group that was on the original server, we assume that this will be done prior to running this script.
The example below will demonstrate how to recreate the filesystems that were on the volume group name "datavg".
{: .text-justify}

**Here is the output file that was on produced on "gotham" server:** 

```bash
$ cat $SADMIN/dat/dr/gotham_fs_save_info.dat
# SADMIN - Filesystem Info. for system gotham.Host
# File was created by sadm_dr_savefs.sh on Fri Dec  7 11:13:54 EST 2018
# This file is use in a Disaster Recovery situation
# The data below is use by sadm_dr_recreatefs.sh to recreate filesystems
# ---------------------------------------------------------------------
# 
datavg::swap01:swap:4096:::0000
rootvg::swap00:swap:2048:::0000
rootvg:/:root:ext4:1024:root:root:0555
rootvg:/opt:opt:ext4:1024:root:root:0755
rootvg:/tmp:tmp:ext4:2048:root:root:1777
rootvg:/usr:usr:ext4:7997:root:root:0755
rootvg:/var:var:ext4:2048:root:root:0755
rootvg:/home:home:ext4:30013:root:root:0755
datavg:/coco1:coco1:ext4:128:root:root:0755
datavg:/coco2:coco2:ext3:1024:staff:jacques:0755
datavg:/coco3:coco3:ext4:900:root:root:0755
rootvg:/sadmin:admlv:ext4:1024:sadmin:sadmin:0775
datavg_sdb:/data_sdb:datavgsdblv:ext4:4444:root:root:0755
rootvg:/etc/perf:perf:ext4:128:root:root:0755
rootvg:/usr/local:usrloc:ext4:512:root:root:0755
```

You can modify this file prior to running the script.
- If you don't want a filesystem to be created, you can remove the line or change the volume group name.
- You can also change the name of the filesystem, the size, owner, group or permission.
- You can even change the filesystem type, the script support ext2, ext3, ext4 and xfs.


If we look in our Disaster Recover directory in the lvm file ($SADMIN/dat/dr/gotham_lvm.txt), we can find that :
- The size occupy by the volume group 'datavg' is 15.99G.
- That the volume group 'datavg' is only on one disk.
- That is contain 3 filesystems (/coco1 coco2 /coco3) and one swap file (swap01).

```bash
#-------------------------------------------------------------------------------
# Command: /sbin/pvs
#-------------------------------------------------------------------------------
#
PV         VG         Fmt  Attr PSize  PFree 
/dev/sda2  rootvg     lvm2 a--u 55.75g  4.50g
/dev/sdb1  datavg_sdb lvm2 a--u 15.99g 11.65g
/dev/sdc1  datavg     lvm2 a--u 15.99g  9.99g   <<<<<
/dev/sdd1  data2vg    lvm2 a--u 96.00m 96.00m
#
#-------------------------------------------------------------------------------
# Command: /sbin/vgs
#-------------------------------------------------------------------------------
#
VG         #PV #LV #SN Attr   VSize  VFree 
data2vg      1   0   0 wz--n- 96.00m 96.00m
datavg       1   5   0 wz--n- 15.99g  9.11g     <<<<<
datavg_sdb   1   1   0 wz--n- 15.99g 11.65g
rootvg       1  14   0 wz--n- 55.75g  4.50g
#
#
#-------------------------------------------------------------------------------
# Command: /sbin/lvscan
#-------------------------------------------------------------------------------
#
ACTIVE            '/dev/datavg/coco1' [128.00 MiB] inherit  <<<<<
ACTIVE            '/dev/datavg/coco2' [1.00 GiB] inherit    <<<<<
ACTIVE            '/dev/datavg/coco3' [900.00 MiB] inherit  <<<<<
ACTIVE            '/dev/datavg/swap01' [4.00 GiB] inherit   <<<<<
ACTIVE            '/dev/datavg_sdb/datavgsdblv' [4.34 GiB] inherit
ACTIVE            '/dev/rootvg/home' [29.31 GiB] inherit
ACTIVE            '/dev/rootvg/opt' [1.00 GiB] inherit
ACTIVE            '/dev/rootvg/perf' [128.00 MiB] inherit
ACTIVE            '/dev/rootvg/root' [1.00 GiB] inherit
ACTIVE            '/dev/rootvg/swap00' [2.00 GiB] inherit
ACTIVE            '/dev/rootvg/tmp' [2.00 GiB] inherit
ACTIVE            '/dev/rootvg/usr' [7.81 GiB] inherit
ACTIVE            '/dev/rootvg/usrloc' [512.00 MiB] inherit
ACTIVE            '/dev/rootvg/var' [2.00 GiB] inherit
ACTIVE            '/dev/rootvg/admlv' [1.00 GiB] inherit
```

At Disaster Recovery site, recreate the 'datavg' volume group.
Before running the script, let's recreate the volume group "datavg".

```bash
# pvcreate /dev/sdc1             (Device could be a disk or a partition)
Physical volume "/dev/sdc1" successfully created

# vgcreate datavg /dev/sdc1      (Create VG on the created device)
Volume group "datavg" successfully created

# vgs
VG         #PV #LV #SN Attr   VSize  VFree 
data2vg      1   0   0 wz--n- 96.00m 96.00m
datavg       1   0   0 wz--n- 15.99g 15.99g  (VG is on 1 PV, 0 LV on it and empty)
datavg_sdb   1   1   0 wz--n- 15.99g 11.65g
rootvg       1  14   0 wz--n- 55.75g  4.50g
# 
```        

Once the "datavg" volume group is created, we can now start the script:

```bash
# sadm_dr_recreatefs.sh 
================================================================================
Starting sadm_dr_recreatefs.sh V2.2 - SADM Lib. V2.52
Server Name: gotham.maison.ca - Type: LINUX
CENTOS 6.10 Kernel 2.6.32-754.6.3.el6.i686
==================================================
        
Currently verifying the LVM version installed on system
Validating Program Requirements before proceeding ...

List of the volume group that are present in /sadmin/dat/dr/gotham_fs_save_info.dat
datavg
datavg_sdb
rootvg
        
Enter the volume group name that you want to recreate the filesystems : 
datavg

This is a list of filesystems (and swap) that will created on datavg volume group
Type: swap  Mount Point:                                 LVName: swap01               
Type: ext4  Mount Point: /coco1                          LVName: coco1                
Type: ext3  Mount Point: /coco2                          LVName: coco2                
Type: ext4  Mount Point: /coco3                          LVName: coco3                

Do you want to proceed with the creation of all filesystems on datavg [Y/N] ? Y

Running : /sbin/lvcreate -L4096M -n swap01 datavg
Running : /sbin/mkswap -c /dev/datavg/swap01
Running : /sbin/swapon /dev/datavg/swap01
Running : Adding entry in /etc/fstab
Filesystem  created successfully

Running : /sbin/lvcreate -L128M -n coco1 datavg
Running : /sbin/mkfs.ext4 -b4096 /dev/datavg/coco1
Running : /sbin/fsck.ext4 -f /dev/datavg/coco1
Running : /sbin/tune2fs -c 0 -i 0 /dev/datavg/coco1
Running : /bin/mkdir -p /coco1
Running : Adding entry in /etc/fstab
Running : /bin/mount /coco1
Running : /bin/chown root:root /coco1
Running : /bin/chmod 0755 /coco1
Filesystem /coco1 created successfully

Running : /sbin/lvcreate -L1024M -n coco2 datavg
Running : /sbin/mkfs.ext3 -b4096 /dev/datavg/coco2
Running : /sbin/fsck.ext3 -f /dev/datavg/coco2
Running : /sbin/tune2fs -c 0 -i 0 /dev/datavg/coco2
Running : /bin/mkdir -p /coco2
Running : Adding entry in /etc/fstab
Running : /bin/mount /coco2
Running : /bin/chown jacques:staff /coco2
Running : /bin/chmod 0755 /coco2
Filesystem /coco2 created successfully

Running : /sbin/lvcreate -L900M -n coco3 datavg
Running : /sbin/mkfs.ext4 -b4096 /dev/datavg/coco3
Running : /sbin/fsck.ext4 -f /dev/datavg/coco3
Running : /sbin/tune2fs -c 0 -i 0 /dev/datavg/coco3
Running : /bin/mkdir -p /coco3
Running : Adding entry in /etc/fstab
Running : /bin/mount /coco3
Running : /bin/chown root:root /coco3
Running : /bin/chmod 0755 /coco3
Filesystem /coco3 created successfully

==================================================
Script return code is 0
Script execution time is 00:01:30
Trim History /sadmin/dat/rch/gotham_sadm_dr_recreatefs.rch to 125 lines
Requested alert only if script fail (Won't send alert)
Trim log /sadmin/log/gotham_sadm_dr_recreatefs.log to 1000 lines
Sat Dec  8 11:17:38 EST 2018 - End of sadm_dr_recreatefs.sh
================================================================================
# 
```


### Aix - Recreating the volume group and the filesystems it contain.

Every day when the 'sadm_dr_savefs.sh' script run it create a minimum of two files in $SADMIN/dat/dr directory.
One file is named ${HOSTNAME}_pvinfo.txt and we have another for each volume group present on the server (except 'rootvg').
Let's say for example we have the two files for an Aix server that had 2 volumes groups named 'rootvg' and 'datavg'.
Actually, we want to recover the volume group 'datavg' on another server at the disaster recovery site.
The volume group 'datavg' contained one filesystem with the mount point '/test1'.
{: .text-justify}

The server we have at the disaster recovery site have two disks :
- The first one (hdisk0) is dedicated to the volume group 'rootvg' (the operating system).
- The second one (hdisk1) is not used at the moment and will be use to recover the 'datavg' volume group.

```bash
# lspv
hdisk0      	0002dd2f26946375                	rootvg      	active
hdisk1      	0002dd2f24d98974                	None       	 
```        


To recreate the 'datavg' volume group on disk 'hdisk1', we need to create a file with the diskname used for the restore.
With your favorite editor create a file in '$SADMIN/dat/dr' directory and name it '${HOSTNAME}_${VG}_restvg_disks.txt.
In our example, the file name would be, 'aixb50_datavg_restvg_disks.txt' and would contain only one line.
{: .text-justify}

```bash
# cat $SADMIN/dat/dr/aixb50_datavg_restvg_disks.txt
hdisk1
```

A different file have to be created for each volume group.
This is a simple example, but imagine if you have multiple volume groups and multiple disks, the process is pretty simple.
The thing you should take care of, is that the total disks size of all these disks should be equal or greater than the size of the VG to recreate.
You can find the size you need to allocate in order to recreate the volume group in $SADMIN/dat/dr/HOSTNAME_pvinfo.txt.
{: .text-justify}

Now let's run the script to recreate our volume group and the filesystems in it.

```bash
root@aixb50(/sadmin/bin)# ./sadm_dr_recreatefs.sh
2016.12.02 15:52:24 - =========================================================
2016.12.02 15:52:24 - Starting sadm_dr_recreatefs.sh - Version 2.0 on aixb50
2016.12.02 15:52:25 - AIX AIX 5.3 IBM_AIX
2016.12.02 15:52:25 - =========================================================
2016.12.02 15:52:25 -  
2016.12.02 15:52:25 - AIX RESTORE OF A VOLUME GROUP
2016.12.02 15:52:25 -  
2016.12.02 15:52:25 - A Backup of these VG(s) exist in /sadmin/dat/dr :
datavg
2016.12.02 15:52:25 -  
2016.12.02 15:52:26 - Enter the volume group name that you want to restore :
datavg
2016.12.02 15:52:37 - Based on the content of /sadmin/dat/dr/aixb50_datavg_restvg_disks.txt
2016.12.02 15:52:37 - Here is the list of the destination disk(s) used for the restore
2016.12.02 15:52:37 -  hdisk1
2016.12.02 15:52:37 -  
2016.12.02 15:52:37 -  
2016.12.02 15:52:37 - Now ready to restore volume group datavg using the following disk(s)
2016.12.02 15:52:37 -  hdisk1
2016.12.02 15:52:38 -  
Do you want to proceed with the restore [Y/N] ? y

2016.12.02 15:52:44 - Restoring Volume Group datavg using backup file named :
2016.12.02 15:52:44 - /sadmin/dat/dr/aixb50_datavg.savevg
2016.12.02 15:52:44 -  
2016.12.02 15:52:44 - The backup will be restore onto these disk(s) :
2016.12.02 15:52:44 -  hdisk1
2016.12.02 15:52:44 -  
2016.12.02 15:52:44 - Command running is
2016.12.02 15:52:44 - restvg -q -f/sadmin/dat/dr/aixb50_datavg.savevg  hdisk1 
2016.12.02 15:52:44 -  
Will create the Volume Group:   datavg
Target Disks:   hdisk1
Allocation Policy:
        Shrink Filesystems: 	no
        Preserve Physical Partitions for each Logical Volume:   no
datavg
loglv01
fslv08
New volume on /sadmin/dat/dr/aixb50_datavg.savevg:
Cluster size is 51200 bytes (100 blocks).
The volume number is 1.
The backup date is: Fri Dec  2 14:43:17 EST 2016
Files are backed up by name.
The user is root.
x       	98 ./tmp/vgdata/vgdata.files20540
x       	98 ./tmp/vgdata/vgdata.files
x     	3313 ./tmp/vgdata/datavg/filesystems
x        	0 .
x     	2446 ./tmp/vgdata/datavg/datavg.data
The number of restored files is 6.
x      	341 ./tmp/vgdata/datavg/backup.data
The total size is 6296 bytes.
2016.12.02 15:53:17 -  
2016.12.02 15:53:18 - =========================================================
2016.12.02 15:53:18 - Script return code is 0
2016.12.02 15:53:19 - Script execution time is 00:00:54
2016.12.02 15:53:19 - Trimming /sadmin/dat/rch/aixb50_sadm_dr_recreatefs.rch to 125 lines
2016.12.02 15:53:20 - User requested mail only if script fail - Will not send mail
2016.12.02 15:53:20 - Trimming /sadmin/log/aixb50_sadm_dr_recreatefs.log to max. 5000 lines.
2016.12.02 15:53:20 - Fri Dec  2 15:53:20 EST 2016 - End of sadm_dr_recreatefs.sh
2016.12.02 15:53:20 - =========================================================
2016.12.02 15:53:20 -  
root@aixb50(/sadmin/bin)#
```

After the restore, with can see that the volume group 'datavg' have been recreated on 'hdisk1'.
We had the filesystem '/test1' on that volume group and it as been also recreated.
{: .text-justify}

```bash
        root@aixb50(/sadmin/bin)# lspv
        hdisk0      	0002dd2f26946375                	rootvg      	active
        hdisk1      	0002dd2f24d98974                	datavg      	active
        root@aixb50(/sadmin/bin)#
        root@aixb50(/sadmin/bin)# lsvg
        rootvg
        datavg
        
        root@aixb50(/sadmin/bin)# lspv -l hdisk1
        hdisk1:
        LV NAME           	LPs 	PPs 	DISTRIBUTION      	MOUNT POINT
        fslv08            	3   	3   	00..03..00..00..00	/test1
        loglv01           	1   	1   	00..01..00..00..00	N/A
        
        root@aixb50(/sadmin/bin)# df /test1
        Filesystem	512-blocks  	Free   %Used	Iused %Iused Mounted on
        /dev/fslv08   	393216	    392496	1%    	4 	    1%  /test1
        
        root@aixb50(/sadmin/bin)# ls -l /test1
        total 0
        drwxr-xr-x	2 root 	system      	256 Dec 02 15:53 lost+found
```

it is worth mentioning that raw devices are included in the backup and are restore by this script.

[Back to the top](#top_of_page)

{% include {{ site.section_options     }} %}
| **-i** | option -i | 

{% include {{ site.section_environment }} %}

{% include {{ site.section_exitcode    }} %}

{% include {{ site.section_author      }} %}

{% include {{ site.section_copyright   }} %}


<a id="seealso"></a>
## SEE ALSO
[sadm_dr_savefs.sh]({% post_url 2021-06-02-sadm-dr-savefs %}) - Save system filesystems information in order to recreate them from scratch.  
[sadm_client_sunset.sh]({% post_url 2021-05-31-sadm-client-sunset %}) - Clients end of day housekeeping and producing system information files  
[sadm_client_housekeeping.sh]({% post_url 2021-05-29-sadm-client-housekeeping %}) - Purge old log,rch,nmon files and check $SADMIN permission   
[sadm_create_sysinfo.sh]({% post_url 2021-04-22-sadm-create-sysinfo %}) - Collect hardware & software information about the system   
[System Information File]({% post_url 2021-05-30-sysinfo-file %}) - Documentation about the system information file  
[sadm_cfg2html.sh]({% post_url 2021-06-01-sadm-cfg2html %}) - Get System information and creates a HTML web page of it.  
