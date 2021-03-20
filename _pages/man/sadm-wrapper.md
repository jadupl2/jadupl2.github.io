---
title:          sadm_wrapper.sh
layout:         single
date_created:   2008-02-11
date_updated:   2009-02-12 
limit:          1
paginate:       false
show_excerpts:  false
entries_layout: list
author_profile: true

tags:           sadm_wrapper script 
categories:     manpage scripts 
toc:            true
---

Date created : {{ page.date_created }}
Date updates : {{ page.date_updated }}


 We have included four templates that are ready to use :

    One template for shell scripting ($SADMIN/bin/sadm_template.sh).
    Another script template in Python ($SADMIN/bin/sadm_template.py).
    The third one is a template for building menu in terminal mode ($SADMIN/bin/sadm_template_menu.sh).
    Last but not least, the SADMIN wrapper allow you to execute your existing scripts and benefits right away of the SADMIN tools ($SADMIN/bin/sadm_wrapper.sh).



Using the wrapper to run your existing scripts and benefits of the SADMIN tools

    First let's create our test script, with the editor of your choice, create the file $SADMIN/usr/bin/show_date.sh

        
        /sadmin/usr/bin$ vim show_date.sh 
        #! /usr/bin/env sh
        echo "Today is `date`"
        /sadmin/usr/bin$ 
        


    Let's run our script using the SADMIN wrapper.

        
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
        


    We should now have a log let's look at it.

        
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
        


    We should now have a RCH file that was created too.

        
        /sadmin/usr/bin$ cat $SADMIN/dat/rch/holmes_show_date.rch 
        holmes 2018.11.03 13:47:37 .......... ........ ........ show_date default 2
        holmes 2018.11.03 13:47:37 2018.11.03 13:47:37 00:00:00 show_date default 0
        /sadmin/usr/bin$ 
        


    Really simple don't you think ? 