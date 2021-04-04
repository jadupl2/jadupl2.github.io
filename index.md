---
layout: single
limit: 1
paginate: false
show_excerpts: false
entries_layout: list
author_profile: true
classes: wide
---

<a name="top_of_page"></a> 

![sadm_text](/assets/img/logo/sadmin_logo_88x88.png "SADMIN Logo")
![sadm_logo](/assets/img/logo/sadmin_text_343x93.png "SADMIN Text Logo")


If you're a Unix system administrator who is taking care of multiple servers, you probably 
created some scripts to help you keeping your environment stable and under control. 
With SADMIN you can be notified when something goes wrong, when a script fail or just to let you 
know that your script ran with success. You can received notification via email, SMS or the
Slack application. 
SADMIN can surely help you improve and standardize the administration of your server farm.
{: .text-justify}

![monitor](/assets/img/index_monitor.png "SADMIN monitor page")

**Monitor your scripts from just one place**
* View the [status of all your scripts](/assets/img/webui/scripts_status.png) that run in your server farm.
* View your script log directly from the [web interface](/assets/img/webui/view_logs.png) or from the [command line](/assets/img/cmdline/cat_log.png).
* When a script fail or succeed, can receive a notification by ['SMS/Texto'](/assets/img/sms/textbelt_step10_sms_receive.png), ['Slack'](/assets/img/slack/slack_warning.png) or by [email](/assets/img/mail/sysmon_mail_notification.png).


<br>

**Create/Modify your scripts using our templates**  
* Use our [Shell](/_pages/man/sadm-template-sh) and [Python](_pages/man/sadm-template-py) 
templates to create new scripts and benefit of SADMIN tools.  
* Use [SADMIN wrapper](/_pages/man/sadm-wrapper) and *run your existing scripts using the SADMIN tools*.  
  `$SADMIN/bin/sadm_wrapper.sh $SADMIN/usr/bin/yourscript.sh`  
* Starting and ending time of each script along with the exit status is recorded in a 
[history file](/assets/img/files/rch_file_format.png). 

<br>

**Create an inventory of your systems (Linux,Aix,MacOS)**
* Add, [update](/assets/img/webui/server_static_info.png) or delete system in your inventory.
* It collect [system configuration](/assets/img/webui/server_information.png) and [performance data](/assets/img/perfo/rrd_update_cpu_graph.png) of your systems.
* Access all this information from a [web interface](/assets/img/webui/main_screen.png) or from the command line.
* View your servers farm [subnet utilization](/assets/img/webui/view_subnet.png) and see what IP are free to use.  

![SubnetInfo](/assets/img/webui/view_subnet.png "SADMIN Subnet Information")

<br>

**Use the Web Interface to administrate your server farm**  
The web interface is available at http://sadmin.YourDomainName or http://YourSadminServerName  

* For http://sadmin.YourDomainName to work, it must be define in your DNS or /etc/hosts file.
* Use it to add, update and delete server in your server farm.
* View performance graph of your servers up to two years in the past.
* Have your servers configuration on hand, usefull in case of a Disaster Recovery.

<br>

**Help you keeping up to date with O/S update**.
  * Choose when and what system get updated.
  * Choose [date and time to perform the update](/assets/img/webui/osupdate_screen.png).
  * Choose to reboot or not your system after the update.
  * Choose to be notify by 'Slack', SMS or Email if something goes wrong.

<br>

**Backup your important directories and files to a NFS server**
  * Choose what to backup, what to exclude and [how many copies to keep](/assets/img/backup/backup_options.png).
  * Backup directory structure automatically [daily, weekly, monthly and yearly](/assets/img/backup/backup_tree.png) created.
  * Decide when is [the right time to perform the daily backup](/assets/img/backup/backup_screen.png).
  
<br>

**Easy installation**
  * Untar the download file into the directory of your choice (We recommend /opt/sadmin).
  * Run the [setup.sh](_pages/man/sadm-setup-sh) script, answer a few questions and that's it.
    * Once the installation is finish, just type 'http://sadmin' in your web browser.
    * Server installation install/configure the Apache Web server and MariaDB server.
    * See the SADMIN requirements on this [page](/_pages/requirements).
    * Cron jobs (/etc/cron.d) will take care of keeping SADMIN healthy.  
  * After running the setup script, Impatient user may want to read the [Quick start guide](/_pages/quickstart).

[Back To The Top](#top_of_page)

<br>

---

## Run on most popular Linux distributions

* The **SADMIN client** have been tested to work on Redhat, Fedora, CentOS, Debian, Ubuntu, Raspbian and Aix, but it should work on most Linux distribution.
* The **SADMIN server**  is only supported Redhat, CentOS, Debian, Ubuntu and Raspbian. 
* Install time is about 10 minutes.
* We have been working for more than three years on these tools and it's getting pretty stable. 
* We will continue to add and enhance the SADMIN tools over the years to come.  

[Back To The Top](#top_of_page)

<br>

---

## Download

* Download the latest version of the SADMIN Project from our [download page](/_pages/download).
* Have a look at our [changelog](/_pages/changelog) and see the latest features.
* You can also clone the project from [GitHub](https://github.com/jadupl2/sadmin)
    * `git clone https://github.com/jadupl2/sadmin.git`  

[Back To The Top](#top_of_page)


<br>

---

## Installing SADMIN Tools

### Method 1 : Cloning our git repository (Recommended)

```bash
    Change directory to /opt
    # cd /opt

    Clone the SADMIN repository from GitHub
    # git clone https://github.com/jadupl2/sadmin.git  

    Run the setup program
    # /opt/sadmin/setup/setup.sh
```

### Method 2 : Using the downloaded 'tgz' file

```bash
    Change directory to /opt
    # cd /opt

    Create a filesystem or directory where you want SADMIN to be install
    # mkdir /opt/sadmin

    Copy the latest version of SADMIN file you have downloaded in '/opt' directory.
    # cp sadmin_xx.xx.xx.tgz /opt

    Change directory to '/opt/sadmin' directory
    # cd /opt/sadmin

    Untar the file
    # tar -xvzf ../sadmin_xx.xx.xx.tgz

    Run the setup program
    # /opt/sadmin/setup/setup.sh
```

See our information page about [running the setup script](/_pages/man/sadm-setup-sh).

[Back To The Top](#brief-description)

<br>

---

## SADMIN Support
Should you ran into problem while installing or running the SADMIN tools, please run the 
'sadm_support_request.sh', attach the resulting file to an email with a description of your 
problem or question and sent it to <sadmlinux@gmail.com>.
We will get back to you as soon as possible.

[Back To The Top](#top_of_page)

<br>

---

## Copyright and license
The SADMIN is a collection of free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version. 

The SADMIN Tools is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  

See the [LICENSE](LICENSE) file for details.

[Back To The Top](#top_of_page)

<br>

---

[1]: https://www.sadmin.ca/img/logo/sadmin_small_logo.png
