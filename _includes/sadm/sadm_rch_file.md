## The [R]esult [C]ode [H]istory (.rch) file

### The RCH file format
The Result Code History file, is a simple text file used to record some information and 
statistics at the end of each script. With the information included in this file we can see
the date and time the script was started, when it ended and did it finish with success or failure.
We can also determine if a notification should be sent, who to send it and how to send it with
the use of the alert group included on the line. 
Below is an example of what a RCH file look like.
{: .text-justify}
```
holmes 2021.04.05 13:32:18 2021.04.05 13:32:22 00:00:04 sadm_template default 1 0
```
First we have the *host name* where the script was executed, then the *date and time it started and
finished*, followed by the *elapse execution time* of the script. The seventh field is the *script
name* (without extension) and then the *alert group* that the notification (alert) would be sent. 
>The ninth field is the *alert type*, it determine what to do with the success or the failure of the script.   
> '0' mean never send an alert, whether the script was a success or not.  
> '1' mean if the script terminated with an error, send an alert.  
> '2' mean if the script terminated with success, send an alert.  
> '3' mean always send an alert whether the script was a success or not.   

The last column indicate the script *termination status*, '0' mean success and a '1' a failure. 
It is important to know, that when a script fail it will always appear as failed in the SADMIN 
Web Monitor page as failed. It will stay on the monitor page until it run again and terminate 
with success or that you edit the 'RCH' file on the system that generated the error and remove 
the error line or change the last column from '1' to '0'. 
{: .text-justify}


### Do I want to use RCH file or not

By default, every time you execute a script that's using the SADMIN Tools, there will be a
line is added to the history file. If the file doesn't exist it will be created. If the script 
failed, normally you get a notification (alert) by email, by SMS or by Slack. There are time when
you don't want to be alerted whatever the result of a script is. For example, if you created an 
interactive script you may not care about the exit code, you can then disable usage of the RCH file. 
In this situation, you can set variable '**SADM_USE_RCH**' to 'N' in the 
[SADMIN definition section](#sadmin_shell_section) of the script.  
{: .text-justify}

```bash
export SADM_USE_RCH="N"  # Generate or not Entry in Result Code History file`  
```  


### The History file name convention

The history file name (.rch) is prefix by the hostname, an underscore and followed by the script 
name and have an extension of '.rch'. Let's assume we are on a host named 'holmes' and the script 
name is 'helloWorld', so the history file name will be 'holmes_helloWorld.rch'. The RCH file 
are created in the SADMIN data directory '**$SADMIN/dat/rch**'.
{: .text-justify}


### RCH files automatically transferred to SADMIN Server

The SADMIN server collect every history files created or modified on every clients at regular 
interval (every 5min via a cron job in /etc/cron.d/sadm_server). It is one of the responsibility 
of script '[sadm_fetch_client.sh](/_pages/man/sadm_fetch_client)' to transfer any history changed 
to the SADMIN server. Information included in this file will be visible from the Web interface 
and from the command line on the SADMIN server. It is also be used to trigger an alert, if you
requested it.
{: .text-justify}


### Controlling the history file size  

Depending how frequently you run a particular script you may want to control the size of 
the history file. If you run a script on a daily basis and you want to keep one month of history,
then you may want to keep around 31 linus in the 'RCH' file. To same some disk space and to keep 
transfer time to a minimum, you can control the number of lines you want to keep in each history 
file. The default maximum number of lines to keep in the '.rch' file is 35 lines and it's taken 
from the SADMIN configuration file ($SADMIN/cfg/sadmin.cfg).  
{: .text-justify}

```bash
SADM_MAX_RCHLINE=35
```   

You can override this default by changing '**SADM_MAX_RCLINE**' variable in the [SADMIN definition section](#sadmin_shell_section) of your script.   

```bash
`export SADM_MAX_RCLINE=31     # When Script End Trim rch file to 31 lines   
```

If you don't want to trim the history file for a particular script, then set the '**SADM_MAX_RCLINE**' 
variable to '0' in the [SADMIN definition section](#sadmin_shell_section) .   

```bash
export SADM_MAX_RCLINE=0       # Don't trim the history file (.rch) 
```

### [R]esult [C]ode [H]istory File Summary

![rch_file_format.png](/assets/img/files/rch_file_format.png "SADMIN rch_file_format"){: .align-center}

