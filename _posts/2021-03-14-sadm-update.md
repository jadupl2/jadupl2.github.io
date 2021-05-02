---
title:          Updating SADMIN Tools
desc:           Update to latest version of SADMIN
version:        2.2
date:           2021-03-14
updated:        2021-04-22
os:             Linux, Aix, MacOS
tags:           [ utilities ] 
categories:     [ utilities ] 
#
layout:         single
search:         true
author_profile: false
toc:            false
classes:        wide
sidebar:
  title: "Documentation"
  nav: sidebar-manpage
---

<font size="3">
<div>Version v{{ page.version }} - Updated {{ page.updated }}</div>
<div>Run on {{ page.os }}</div>
</font>


## Method 1 (Recommended)
To always get the latest version of SADMIN, use the 'git pull' command. Your Database and the
 change you made to your configuration files in "$SADMIN/cfg" will not modified at all. This 
 method will allow you to get the latest version of the SADMIN tools.
{: .text-justify}

```bash
# cd $SADMIN
# /opt/sadmin # git pull origin master
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


{% include {{ site.section_author      }} %}

{% include {{ site.section_copyright   }} %}


<a id="seealso"></a>
## SEE ALSO

[SADMIN installation](/_pages/install.md) - SADMIN installation page.    
