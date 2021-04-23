---
title:              sadm_wrapper.sh
layout:             single
date_created:       2018-02-11
date_updated:       2021-03-12 
version:            1.6
show_excerpts:      false
entries_layout:     list
tags:               tools
categories:         utilities 
author_profile:     false
toc:                false
classes:            wide
sidebar:
  title:            "Documentation"
  nav:              sidebar-manpage
---

Date created : {{ page.date_created }}
Date updates : {{ page.date_updated }}


### Create a test script

First let's create our test script, with the editor of your choice, create the file $SADMIN/usr/bin/show_date.sh

{% highlight bash %}
/sadmin/usr/bin$ vi show_date.sh   
#! /usr/bin/env sh  
echo "Today is `date`"   
{% endhighlight %}        


### Using the SADMIN wrapper

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
        


## View the script generated log
       
{% highlight bash %}
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
{% endhighlight %}
        

### View the generated Result Code History (*.rch) file

{% highlight bash %}
/sadmin/usr/bin$ cat $SADMIN/dat/rch/holmes_show_date.rch 
holmes 2018.11.03 13:47:37 .......... ........ ........ show_date default 2
holmes 2018.11.03 13:47:37 2018.11.03 13:47:37 00:00:00 show_date default 0
/sadmin/usr/bin$ 
{% endhighlight %} 
        


Really simple don't you think ? 
{: .notice--warning}