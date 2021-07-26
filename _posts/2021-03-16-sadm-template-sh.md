---
title:              Using SADMIN Shell script template
desc:               How-to use shell script template
version:        2.2
date_updated:       2021-05-05 
os:             Linux, Aix, MacOS
type:           D  # [D]oc [S]=Server only [C]=Client [B]oth
tags:               [ templates ]
categories:         [ templates ]
sadm_section_sh:    sadm/sadm_section_sh.md
sadm_file_rch:      sadm/sadm_rch_file.md
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

{% include sadm/sadm_page_info.md %}

## What's in the shell script template  
The shell script template ($SADMIN/bin/sadm_template.sh) is ready to use. You can run it now, 
by issuing the following command; '**$SADMIN/bin/sadm_template.sh**'. We will demonstrate later on,
what is included in the template and what are the benefits of using it. The best way to learn 
how to use the SADMIN tools, is to create a script from the template and this is what we will
demonstrate later on on this page.  
{: .text-justify}

This template include two main functions, the '**process_servers()**' and the '**main_process()**'.  
![sadm_template_sh_03.png](/assets/img/sadm_template_sh_03.png "Main Template functions")

- The '**main_process()**' is normally use when you're writing a script that don't need 
any SADMIN database information. By default, the 'main_process()' is activated, but you decide
which one you need for the script you're starting.  
![sadm_template_sh_main_process.png](/assets/img/sadm_template_sh_main_process.png "main_process() Template functions")

- In the Shell Script template, you will also find a function that demonstrate how to access the 
information in the server database. The '**process_servers()**' can be use when you need to 
perform action based on the content of the server database. It actually build a list of all 
active systems (active field set to true) and test the 'ssh' to each of the servers. To use it, 
just remove the '#' in front of the 'process_server' line. Running the script won't harm 
anything, so can run it to see it in action.
{: .text-justify}


## The template script include three things

1- The [SADMIN definition section](#sadmin_shell_section), you will find near the beginning of 
the template shell script, a code section that is require to use the SADMIN tools, we will 
call it the 'SADMIN Section'. This is where defined and set variables that will influence the 
behavior of the library. Of course you can use them within your script. This is where the shell 
library is loaded. for a list of all the library functions and variables that are available 
to you, please visit the [Shell Library page](/_pages/man/sadmlib_std_sh).
{: .text-justify}

{% include {{ page.sadm_section_sh }} %}


2- The call to the '**sadm_start**' function to initialize SADMIN environment
```bash
# Call SADMIN Initialization Procedure
sadm_start                                              # Init Env Dir & RC/Log File
if [ $? -ne 0 ] ; then sadm_stop 1 ; exit 1 ;fi         # Exit if Problem 
```        

3- The call to the '**sadm_stop**' function at the end of your script (With one parameter, 
'0' = Success or a non-zero value = Error).
```bash
# Your Main process procedure
main_process                                            # Main Process
SADM_EXIT_CODE=$?                                       # Save Process Return Code 

SADM_EXIT_CODE=$?                                       # Save Process Return Code 
sadm_stop $SADM_EXIT_CODE                               # Close/Trim Log & Del PID
exit $SADM_EXIT_CODE                                    # Exit With Global Err (0/1)
```        


## Example using the template

First thing to do is to make a copy of the template shell script, into the user (usr/bin) 
directory, so it won't be touch by subsequent release update.  
```bash
$ cp $SADMIN/bin/sadm_template.sh $SADMIN/usr/bin/helloWorld.sh`  
```
You should never modify the original template, always make a copy and use the copy.
You will use it more than once and it could get overwritten when updating to a newer version 
of SADMIN. The user directory ($SADMIN/usr) is the right place to put any new script you create.
This directory ($SADMIN/usr) will never be modified by newer version of SADMIN.
{: .text-justify}

To create our first 'Hello World' shell script using SADMIN tools, with the editor of your 
choice just add the line below in the function called 'main_process()' of your new 
script "helloWorld.sh".

```bash
sadm_write "Hello World\n"
```

One of the function included in the SADMIN Shell Library is "sadm_write()". By default, it 
write the string it received to the screen and to the script log. But you can modify this 
behavior, by modifying the variable "SADM_LOG_TYPE" in SADMIN section.  
```bash
export SADM_LOG_TYPE="B"             # Write goes to [S]creen [L]ogFile [B]oth`   
```


### Let's run our script now and see the output we get.
![sadm_template_sh_06.png](/assets/img/sadm_template_sh_06.png "Output of sadm_template.sh")

 
## The Script Header

The script header, is a block of information about the script you are running. The script header 
is generated automatically by the SADMIN tools shell library. Normally, it is shown of the screen 
and recorded with a time stamp in the script log.   
   
![sadm_template_sh_header.png](/assets/img/sadm_template_sh_header.png "Script Header Example"){: .align-center}

The script header is created by the '**sadm_start()**' function that is part of the SADMIN Shell 
Library. By default, every script using SADMIN library will output (Log and Screen) a script 
header. Unless you set the variable '**SADM_LOG_HEADER**' to 'N' in the SADMIN Section.  
{: .text-justify}

```bash
export SADM_LOG_HEADER="Y"      # Y=ProduceLogHeader N=NoHeader`  
```


The second line of the header show the date, the script name and version and the SADMIN library 
version. You set *your script version number* in the [SADMIN section](#sadmin_shell_section) of the script. 

```bash
export SADM_VER='1.0'           # Your Current Script Version`  
```

The Library version is available to you via a read only variable called "**$SADM_LIB_VER**". The 
next line, show the system name (FQDN) and the system type (LINUX,AIX,DARWIN). The fourth line 
show the distribution name, it's version number and version of the kernel


 
## The Script Footer

The script footer, is a block of information about the script that just ended. It is automatically 
generated by the SADMIN tools shell library when the '**sadm_stop()*' function is called. Normally, 
it is shown of the screen and recorded with a time stamp in the script log. 

![sadm_template_sh_footer.png](/assets/img/sadm_template_sh_footer.png "Script Footer Example"){: .align-center}

By default, the footer is generated, unless you set the variable '**SADM_LOG_FOOTER**' to 'N' 
in the SADMIN section.  

```bash
    export SADM_LOG_FOOTER="N"      # [Y]=Include Log Footer [N]=No log Footer
```

The first line show the exit code of the script (0=Success 1=Error) and the execution time of 
the script (HH:MM:SS). The second line show the name of the [R]eturn [C]ode [H]istory file and 
the maximum of lines, you decided to have in it. The next two lines inform you if an alert will 
be send or not and the name of the alert group that it to which it would send it. Just after 
come the log line, that give us the log file name and state that is was appended to previous 
content or a new log was created. The last line show the name of the script and the date and 
time it as terminated.
{: .text-justify}


## Controlling the script Header and Footer output

To suppress header/footer from log and screen, change "**SADM_LOG_FOOTER**" and 
"**SADM_LOG_HEADER**" variable from "Y" to "N".   
![sadm_template_sh_20.png](/assets/img/sadm_template_sh_20.png "Portion of SADMIN Section")

As you can see now the header and footer doesn't appear anymore on the screen (and in the log of the script).  
![sadm_template_sh_24.png](/assets/img/sadm_template_sh_24.png "Output with No Header & Footer") 



<br>
{% include {{ page.sadm_file_rch }} %}



## The script log file

When a script using the SADMIN Tools is executed, there is a log file that is created or updated.
All scripts logs are created in the "**$SADMIN/log**" directory. The log file name is prefix by 
the host name, an underscore and  followed by the script name and have an extension of '.log'. 
For example, if the host name is '*holmes*', the script name is '*helloWorld*', then the log 
name will be '*holmes_helloWorld.log*'.
{: .text-justify}


### Log files automatically transferred to SADMIN Server

The SADMIN server collect every log files created or modified on every clients at regular 
interval (every 5min via a cron job in /etc/cron.d/sadm_server). It is one of the responsibility 
of script '[sadm_fetch_clients.sh](/_pages/man/sadm_fetch_client)' to transfer any '*.log' changed 
to the SADMIN server. Information included in this file will be visible from the Web interface 
and from the command line on the SADMIN server. 
{: .text-justify}


### Controlling the log file size  

The log of a script can be cumulative or a new one can be created at each execution. The default in 
the template is set to created a new log file at each execution (SADM_LOG_APPEND="N"). 
But if you want your script log to be cumulative, then set the SADM_LOG_APPEND="Y" to "Y".
{: .text-justify}  

```bash
    export SADM_LOG_APPEND="Y"     # [Y]=Append Existing Log [N]=Create New One
```

By default the log file is trim at the end of each execution. The log file is trim to the number 
of line specified in $SADMIN/cfg/sadmin.cfg by the variable 'SADM_MAX_LOGLINE' (default 500). You 
can override this default by changing 'SADM_MAX_LOGLINE' variable in the SADMIN Section of your script.  
{: .text-justify}

```bash
    export SADM_MAX_LOGLINE=500   # At end of script Trim log to 500 Lines  
```


### Example of a log file   

![sadm_template_sh_30.png](/assets/img/sadm_template_sh_30.png "Log Output Example")    

<br>
   
### Scripts view from the web interface   
  
![sadm_template_sh_34.png](/assets/img/sadm_template_sh_34.png "Web view of example script")  
  

### Viewing the log from the web interface
![sadm_template_sh_42.png](/assets/img/sadm_template_sh_42.png "Web view of script log")

### Viewing the History file (RCH) from the web interface
![sadm_template_sh_38.png](/assets/img/sadm_template_sh_38.png "Web view of script rch file") 


### Viewing all systems history (.rch) files from the command line  
For more information on this command line script, see the man page of [srch](/_pages/man/sadm_show_rch).

```bash
# srch  
```
![sadm_template_sh_45.png](/assets/img/sadm_template_sh_45.png "Command line view of our scripts")  

