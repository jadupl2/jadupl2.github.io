---
layout: posts
title: Quick Start
limit: 1
paginate: true
show_excerpts: false
entries_layout: list
author_profile: true
---

## Create your own script using SADMIN library
To create your own script using the SADMIN tools, you may want to take a look at the templates, run them and view their code.
Check our tutorial page on using the [shell template](/_pages/man/sadm-template-sh) for a full example.

### Shell script template

Running the template below, will show the kind of [output we get on the screen](/assets/img/cmdline/sadm_template_output_screen.png), but also [the log](/assets/img/cmdline/sadm_template_output_log.png) that is generated along with [Result Code History file (.rch)](/assets/img/cmdline/sadm_template_output_rch.png).

{% highlight bash %}
$SADMIN/bin/sadm_template.sh   
{% endhighlight %} 


### Python script template

{% highlight bash %}
$SADMIN/bin/sadm_template.py   
{% endhighlight %} 


By looking at the output you will notice that we get almost the same look, this is what we wanted, standardize the usage and the output. The Shell and the Python library have almost the same functions and both react the same way.
For example, to create your own shell script :

    cp $SADMIN/bin/sadm_template.sh $SADMIN/usr/bin/newscript.sh

modify it to your need, run it and see the results.


Learn how to use SADMIN Libraries by running the demos

    $SADMIN/bin/sadmlib_std_demo.sh (See output)
    $SADMIN/bin/sadmlib_std_demo.py (See output)


## Use SADMIN wrapper and run your existing using the SADMIN tools

    $SADMIN/bin/sadm_wrapper.sh $SADMIN/usr/bin/yourscript.sh


Use the Web Interface to administrate your server farm
The Web interface is available at http://sadmin.YourDomainName or http://YourSadminServerName

    For http://sadmin.YourDomainName to work, it must be define in your DNS or /etc/hosts file.
    Use it to add, update and delete server in your server farm.
    View performance graph of your servers up to two years in the past.
    If you want, you can automatically update your server O/S at the time and day you scheduled.
    Have server configuration on hand, usefull in case of a Disaster Recovery.
    View your servers farm subnet utilization and see what IP are free to use.
    There's still a lot more to come.

This is it, you are now ready the use the SADMIN tool.

## SADMIN Support
If you ever ran into problem while installing or running the SADMIN tools, please run the 'sadm_support_request.sh', attach the resulting log to an email with a description of your problem or question and sent to support@sadmin.ca. We will get back to you as soon as possible. 
