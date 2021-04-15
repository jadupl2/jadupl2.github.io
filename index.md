---
layout:         single
limit:          1
paginate:       false
show_excerpts:  false
entries_layout: list
author_profile: true
classes:        wide
toc:            false

---

<a name="top_of_page"></a> 

![sadm_text](/assets/img/logo/sadmin_logo_88x88.png "SADMIN Logo")
![sadm_logo](/assets/img/logo/sadmin_text_343x93.png "SADMIN Text Logo")


If you're a Unix system administrator who is taking care of multiple servers, you probably 
created some scripts to help you keeping your environment stable and under control. SADMIN can 
help you by centralizing your scripts logs in one place, by viewing their results in one place and
you can even can be notified if something goes wrong. With SADMIN you can be notified, when a 
script fail or just to let you know that your script ran with success. You can received 
notification via email, SMS or the Slack application. 
SADMIN can surely help you improve and standardize the administration of your server farm.
{: .text-justify}

![monitor](/assets/img/index_monitor.png "SADMIN monitor page")

## Monitor your scripts from just one place
* View the [status of all your scripts](/assets/img/webui/scripts_status.png) that run in your server farm.
* View your script log directly from the [web interface](/assets/img/webui/view_logs.png) or from the [command line](/assets/img/cmdline/cat_log.png).
* When a script fail or succeed, can receive a notification by ['SMS/Texto'](/assets/img/sms/textbelt_step10_sms_receive.png), ['Slack'](/assets/img/slack/slack_warning.png) or by [email](/assets/img/mail/sysmon_mail_notification.png).



## Using our templates 
* Use our [Shell](/_pages/man/sadm-template-sh) and [Python](_pages/man/sadm-template-py) 
templates to create new scripts and benefit of SADMIN tools.  
* Use [SADMIN wrapper](/_pages/man/sadm-wrapper) and *run your existing scripts using the SADMIN tools*.  
  `sadm_wrapper.sh $SADMIN/usr/bin/yourscript.sh`  
* Starting and ending time of each script along with the exit status is recorded in a 
[history file](/assets/img/files/rch_file_format.png). 



## Inventory of your systems
* Add, [update](/assets/img/webui/server_static_info.png) or delete system in your inventory.
* It collect [system configuration](/assets/img/webui/server_information.png) and [performance data](/assets/img/perfo/rrd_update_cpu_graph.png) of your systems.
* Access all this information from a [web interface](/assets/img/webui/main_screen.png) or from the command line.
* View your systems farm [subnet utilization](/assets/img/webui/view_subnet.png) and see what IP are free to use.  

![SubnetInfo](/assets/img/webui/view_subnet.png "SADMIN Subnet Information")



## Web Interface to administrate your systems
* Use it to add, update and delete server in your server farm.
* View [performance graph of your servers up to two years in the past](assets/img/perfo/sadm_perf_adhoc.png).
* Have your systems configuration on hand, useful in case of a Disaster Recovery.
* View all your scripts logs and history files from the web interface.



## Automate your system update
* Choose when and what system are updated.
* Choose [date and time to perform the update](/assets/img/webui/osupdate_screen.png).
* Choose to reboot or not your system after the update.
* Choose to be notify by ['SMS/Texto'](/assets/img/sms/textbelt_step10_sms_receive.png), 
['Slack'](/assets/img/slack/slack_warning.png) or by 
[email](/assets/img/mail/sysmon_mail_notification.png) if something goes wrong.



## Backup to a NFS server
Choose what to backup, what to exclude and [how many copies to keep](/assets/img/backup/backup_options.png).
Backup directory structure automatically [daily, weekly, monthly and yearly](/assets/img/backup/backup_tree.png) created.
Decide when is [the right time to perform the daily backup](/assets/img/backup/backup_screen.png).
{: .text-justify}  


## Run on popular Linux distributions

The **SADMIN client** have been tested to work on Redhat, Fedora, CentOS, Debian, Ubuntu, Raspbian
and Aix, but it should work on most Linux distribution. The **SADMIN server**  is supported 
Redhat, CentOS, Debian, Ubuntu and Raspbian. The installation can normally done within 10 minutes.
We have been working for more than four years on these tools and it's getting pretty stable. We 
will continue to add and enhance the SADMIN tools over the years to come.  
{: .text-justify}

[Back To The Top](#top_of_page)



## Downloading SADMIN Tools
We recommend cloning the SADMIN repository and then run the setup script.  
    * `cd /opt/`    
    * `git clone https://github.com/jadupl2/sadmin.git`    
    * `sudo sadmin/setup/setup.sh`  
Another way is to download the latest version from our [download page](/_pages/download) and have 
a look at our [changelog](/_pages/changelog) and see the latest features. For more information 
about the installation process, view our [install guide](/_pages/install/)
{: .text-justify}

[Back To The Top](#top_of_page)



## SADMIN Support
Should you ran into problem while installing or running the SADMIN tools, please run the 
'sadm_support_request.sh', attach the resulting file to an email with a description of your 
problem or question and sent it to <sadmlinux@gmail.com>.
We will get back to you as soon as possible.
{: .text-justify}

[Back To The Top](#top_of_page)



## Copyright and license
The SADMIN is a collection of free software: you can redistribute it and/or modify it under the 
terms of the GNU General Public License as published by the Free Software Foundation, either 
version 3 of the License, or (at your option) any later version. 
The SADMIN Tools is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; 
without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  
See the [LICENSE](/_pages/license) file for details.  
{: .text-justify}

[Back To The Top](#top_of_page)


[1]: https://www.sadmin.ca/img/logo/sadmin_small_logo.png
