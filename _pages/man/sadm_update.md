---
layout: single
limit: 1
paginate: false
show_excerpts: false
entries_layout: list
author_profile: true
title: Update SADMIN Tools
toc:            true

---


### Method 1  
Use the 'git pull' command (Recommended)

To always get the latest version of SADMIN, use the 'git pull' command (recommended).
```bash
    # cd $SADMIN
    # /opt/sadmin# git pull origin master
    From https://github.com/jadupl2/sadmin
    * branch            master     -> FETCH_HEAD
    Updating 1f8e79d..38034ee
    Fast-forward
    bin/sadm_uninstall.sh | 16 +++++++++-------
    1 file changed, 9 insertions(+), 7 deletions(-)
```

### Method 2  
**Use SADMIN updater**  
Update your system using the SADMIN updater (sadm_updater.sh).
We have a dedicated section for the updater in our manual, take a look at it.
{: .text-justify}


### SADMIN Support  
Should you ran into problem while installing or running the SADMIN tools, please run the 
'sadm_support_request.sh', attach the resulting log to an email with a description of your 
problem or question and sent it to [sadmlinux@gmail.com](mailto:sadmlinux@gmail.com). 
We will get back to you as soon as possible.  
{: .text-justify}
