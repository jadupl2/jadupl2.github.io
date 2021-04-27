---
title:          sadm_wrapper.sh
desc:           Wrapper to run your existing scripts and benefit of SADMIN tools.
version:        1.6
date:           2018-02-11
updated:        2021-03-12 
os:             Linux, Aix, MacOS
tags:           [ tools, wrapper ]
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
<div>$SADMIN/bin/{{ page.title }}</div>
<div>Version v{{ page.version }} - Updated {{ page.updated }}</div>
<div>Run on {{ page.os }}</div>
</font>


<a id="name"></a>

## NAME
{{ page.title }} -- {{ page.desc }}


<a id="synopsis"></a>

## SYNOPSIS

```bash
    {{ page.title }} [-v] [-h] [-d 0-9]  
```


<a id="description"></a>

## DESCRIPTION

First let's create a test script, with the editor of your choice, create the file $SADMIN/usr/bin/show_date.sh

{% highlight bash %}
/sadmin/usr/bin$ vi show_date.sh   
#! /usr/bin/env sh  
echo "Today is `date`"   
{% endhighlight %}        


## Run it using the SADMIN wrapper

{% highlight bash %}
sadmin/usr/bin$ $SADMIN/bin/sadm_wrapper.sh $SADMIN/usr/bin/show_date.sh
================================================================================
Starting show_date.sh V1.6 - SADM Lib. V2.50
Server Name: holmes.maison.ca - Type: LINUX
CENTOS 7.5.1804 Kernel 3.10.0-862.14.4.el7.x86_64
==================================================
 
Executing /sadmin/usr/bin/show_date.sh 
  
==================================================
Script return code is 0
Script execution time is 00:00:00
Trim History /sadmin/dat/rch/holmes_show_date.rch to 125 lines
Requested alert only if script fail (Won't send alert)
Trim log /sadmin/log/holmes_show_date.log to 2000 lines
Sat Nov  3 13:47:37 EDT 2018 - End of show_date.sh
================================================================================
/sadmin/usr/bin$ 
{% endhighlight %}  
        

<a id="examples"></a>

## EXAMPLE

```bash
/sadmin/usr/bin$ cat $SADMIN/log/holmes_show_date.log
 
2018.11.03 13:47:37 ================================================================================
2018.11.03 13:47:37 Starting show_date.sh V1.6 - SADM Lib. V2.50
2018.11.03 13:47:37 Server Name: holmes.maison.ca - Type: LINUX
2018.11.03 13:47:37 CENTOS 7.5.1804 Kernel 3.10.0-862.14.4.el7.x86_64
2018.11.03 13:47:37 ==================================================
2018.11.03 13:47:37  
2018.11.03 13:47:37   
2018.11.03 13:47:37 Executing /sadmin/usr/bin/show_date.sh 
2018.11.03 13:47:37   
Today is Sat Nov  3 13:47:37 EDT 2018
2018.11.03 13:47:37  
2018.11.03 13:47:37 ==================================================
2018.11.03 13:47:37 Script return code is 0
2018.11.03 13:47:37 Script execution time is 00:00:00
2018.11.03 13:47:37 Trim History /sadmin/dat/rch/holmes_show_date.rch to 125 lines
2018.11.03 13:47:37 Requested alert only if script fail (Won't send alert)
2018.11.03 13:47:37 Trim log /sadmin/log/holmes_show_date.log to 2000 lines
2018.11.03 13:47:37 Sat Nov  3 13:47:37 EDT 2018 - End of show_date.sh
2018.11.03 13:47:37 ================================================================================
2018.11.03 13:47:37  
/sadmin/usr/bin$ 
```
        

## View the generated Result Code History (*.rch) file

{% highlight bash %}
/sadmin/usr/bin$ cat $SADMIN/dat/rch/holmes_show_date.rch 
holmes 2018.11.03 13:47:37 2018.11.03 13:47:37 00:00:00 show_date default 1 0
/sadmin/usr/bin$ 
{% endhighlight %} 
        


Really simple don't you think ? 
{: .notice--warning}