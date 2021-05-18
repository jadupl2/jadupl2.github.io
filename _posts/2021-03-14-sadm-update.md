---
title:          Updating SADMIN tools
desc:           Update to latest version of SADMIN
version:        2.2
updated:        2021-05-04
os:             Linux, Aix, MacOS
type:           B  # [S]=Run on Server only, [C]=Client Only, [B]=Run on Both
tags:           [ utilities ] 
categories:     [ utilities ] 
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

<font size="3">
<div>Posted {{ page.date | date: "%Y-%m-%d" }} - Updated {{ page.updated }}</div>
<div>Run on {{ page.os }}</div>
</font>


<br>
**What directories and files will be updated (both method) ?**  
The SADMIN Database and the change you made to your configuration files in “$SADMIN/cfg” will 
not modified at all.

| Directory             | Directory content     | Directory updated         |   
| :---                  | :---                  | :---:                     |   
| sadmin/usr            | Your scripts & data   | No (only usr/mon dir.)    | 
| sadmin/dat            | System data files     | No                        |
| sadmin/log            | Log files             | No                        | 
| sadmin/tmp            | Temp files & PID files| No                        |
| sadmin/cfg            | SADMIN Config files   | No (only dot prefix files)|  
| sadmin/sys            | Start/Shutdown Scripts| No (only dot prefix files)|   
| sadmin/bin            | SADMIN Tools Scripts  | Yes                       |   
| sadmin/lib            | SADMIN Libraries      | Yes                       |   
| sadmin/doc            | SADMIN Documentation  | Yes                       |  
| sadmin/pkg            | Packages we may need  | Yes                       |   
| sadmin/setup          | Installation scripts  | Yes                       |  
| sadmin/www            | Web Interface Directories    | Yes                       |   



## Advantage & Disadvantage of each method

**Method 1**
- To use this method you must have install SADMIN with [method 1 (git clone)](/_pages/install/#git-install).  
- You always have the latest version (Updated frequently).   
- Bug fixes and new features are available sooner.   
- File deletion or rename in $SADMIN are apply to your system instantly.   

**Method 2**   
- You get the latest stable release (Updated less frequently)  
- Can be used to install previous release.  
- File deletion or rename in $SADMIN are done via the housekeeping scripts.  
- Easiest method to update.  
  



<br>
## Method 1 - Using "git pull" (Recommended)
To use this update method, you MUST have used the ["git clone" method (method 1)](/_pages/install/#git-install) 
at installation time. To always get the latest version of SADMIN, use the 'git pull' command. This 
method will allow you to get the latest version of the SADMIN tools. 
{: .text-justify}

1- First we need to check the status of the git repository. Change directory to $SADMIN and enter the
command "git status" like below.

```bash
# cd $SADMIN
/opt/sadmin#
/opt/sadmin# git status
Refresh index: 100% (413/413), done.
On branch master
Your branch is up to date with 'origin/master'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   lib/sadmlib_std.py

no changes added to commit (use "git add" and/or "git commit -a")
```

<br>
2- In the example above, we see from the "git status" result, that the file "lib/sadmlib_std.py" have 
been modified. _But if the the last line of your output is "nothing to commit, working tree clean" 
proceed with the next step._  
- The file "lib/sadmlib_std.py" is part if the SADMIN package and will possibly be updated. As a 
reminder, your shouldn't modify any files that are part of the package, because you 
might miss corrections or enhancements made to SADMIN, but mainly because the change might get 
replace by a future update. But if you need to, move the file in one 
of the "$SADMIN/usr" directories and rename it. Everything in "$SADMIN/usr" (except $SADMIN/usr/mon) 
will never be updated and it is to be used by you.  
- Ok back, to the "git status" result we had. We need to have a clean "git status" before doing our 
'pull' command. To do that, we need to remove the changes you made to the file. To do this we just 
have to do the command below.
{: .text-justify}

```bash
/opt/sadmin# git restore lib/sadmlib_std.py
/opt/sadmin# git status
On branch master
Your branch is up to date with 'origin/master'.

nothing to commit, working tree clean
```

<br>
3- Now that our "git status" is clean, we can now issue our "git pull" command to apply the latest 
SADMIN update.

```bash
/opt/sadmin# git pull --ff-only origin master

remote: Enumerating objects: 45, done.
remote: Counting objects: 100% (45/45), done.
remote: Compressing objects: 100% (9/9), done.
remote: Total 32 (delta 23), reused 32 (delta 23), pack-reused 0
Unpacking objects: 100% (32/32), 5.84 KiB | 106.00 KiB/s, done.
From https://github.com/jadupl2/sadmin
 * branch              master     -> FETCH_HEAD
   90b434ca..49b2ecfa  master     -> origin/master
Updating 90b434ca..49b2ecfa
Fast-forward
 bin/sadm_database_update.py |  96 +++++++++++++++++++++++++++++++++++++++++++++++----
 bin/sadm_rear_backup.sh     |  19 ++++++++--------
 bin/sadm_subnet_lookup.py   |  36 +++++++++++++++++------------
 bin/sadm_template.py        |  23 ++++++++++---------
 cfg/.sadmin.cfg             |  42 ++++++++++++++++++----------------
 lib/sadmlib_screen.sh       |   6 ++---
 lib/sadmlib_std.py          |  20 ++++++++++++-----
 sys/.sadm_startup.sh        | 113 +++++++++++++++++++++++++++++++++++++++++++++++++----
 8 files changed, 202 insertions(+), 153 deletions(-)
```
The command allow you to see what files have been changed since your last update. We can run this 
update process has often as you like, to get the latest fixes and enhancements. You SADMIN Tools is 
now up to date.






<br>
## Method 2 - Extract from a "tar" file 
This is the easiest way to update the SADMIN tools to the a specific version. It can also be used to
restore SADMIN tools to a previous version, if ever ran into a problem. To update is just three 
simple steps: 
{: .text-justify}

1- Download our latest package from the [download page](/_pages/download) and copy it to $SADMIN 
directory.  
2- Change directory to $SADMIN (Where you installed it).  
3- Issue the "tar" command below to extract the SADMIN version to your system.  

None of your configuration files or scripts in $SADMIN/usr and not even the database will be
modified, unless explicitly documented on the download page.  

```bash
/home/jacques/Downloads# mv sadmin_1.3.2.tgz $SADMIN
/home/jacques/Downloads# cd $SADMIN 
/opt/sadmin# tar -xvzf sadmin_1.3.2.tgz 
./
./bin/
./bin/sadm
./bin/sadm_backup.sh
./bin/sadm_backupdb.sh
./bin/sadm_cfg2html.sh
./bin/sadm_client_housekeeping.sh
./bin/sadm_client_sunset.sh
...
...
./www/view/srv/sadm_view_server_info.php
./www/view/srv/sadm_view_servers.php
./www/view/sys/
./www/view/sys/sadm_view_backup.php
./www/view/sys/sadm_view_cfg2html.php
./www/view/sys/sadm_view_rear.php
./www/view/sys/sadm_view_schedule.php
./www/view/sys/sadm_view_sysmon.php
# 
```

There you go, simple enough ? Enjoy ! 



{% include {{ site.section_author      }} %}

{% include {{ site.section_copyright   }} %}


<a id="seealso"></a>
## SEE ALSO

[SADMIN installation](/_pages/install.md) - SADMIN installation page.    
