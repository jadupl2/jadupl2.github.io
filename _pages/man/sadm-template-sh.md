---
title:              Using SADMIN Shell script template
layout:             single
date_created:       2021-03-16
date_updated:       2021-03-16 
limit:              1
paginate:           false
show_excerpts:      false
entries_layout:     list
author_profile:     true
tags:               slack alert scripts
categories:         alert
toc:                false
classes:            wide
sadm_section_sh:    sadm/sadm_section_sh.md
---

<br>
**We have included 3 templates that are ready to use**  
> The [Shell script template](/_pages/man/sadm-template-sh) ($SADMIN/bin/sadm_template.sh).  
> The [Python script template](/_pages/man/sadm-template-py) ($SADMIN/bin/sadm_template.py).    
> The [SADMIN wrapper script](/_pages/man/sadm-wrapper) ($SADMIN/bin/sadm_wrapper.sh) allow you to run your existing script and benefit of the SADMIN tools.  
 

### What's in the shell script template  
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


<br>
### The template script include three things

1- The [SADMIN definition section](/assets/img/sadmin_section_sh.png) at the beginning of the 
template, that set script variables and load the Shell Library.  

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

 
### The Script Header

- The script header is created by the 'sadm_start()' function that is part of the SADMIN Shell Library.
- By default, every script using SADMIN library will output (Log and Screen) a script header.
- Unless you set the variable '**SADM_LOG_HEADER**' to 'N' in the SADMIN Section.  
    ```bash
    export SADM_LOG_HEADER="Y"      # Y=ProduceLogHeader N=NoHeader`  
    ```
- The second line of the header show the date, the script name and version and the SADMIN library version.
  - You set your script version number in the [SADMIN section](/assets/img/sadmin_section_sh.png) of the script. 
    ```bash
    export SADM_VER='1.0'           # Your Current Script Version`  
    ```
- The Library version is available to you via a read only variable called "**$SADM_LIB_VER**".
- The next line, show the system name (FQDN) and the system type (LINUX,AIX,DARWIN).
- The fourth line show the distribution name, it's version number and version of the kernel


 
### The Script Footer
- By default, every script using SADMIN library will produce a script footer.    
  - The footer is generated, unless you set the variable '**SADM_LOG_FOOTER**' to 'N' in the 
SADMIN section.  
    ```bash
    export SADM_LOG_FOOTER="N"      # [Y]=Include Log Footer [N]=No log Footer
    ```
- The second line show the exit code of the script (0=Success 1=Error), the next line show 
the execution time of the script (HH:MM:SS).
- The fourth line show the name of the [R]eturn [C]ode [H]istory file and the maximum of lines, 
you decided to have in it. The default maximum number of lines to keep in the RCH file is 
taken from the SADMIN configuration file ($SADMIN/cfg/sadmin.cfg).   
    ```bash
    SADM_MAX_RCHLINE=125
    ```
- You can override this value for your script by changing the value of the variable in the 
SADMIN Section.  
    ```bash
    export SADM_MAX_RCLINE=100      # When Script End Trim rch file to 125 Lines  
    ``` 
- The next lines inform you if an alert will be send or not, the log file name and the maximum 
of lines, you decided to have in it. 
- The default for the maximum number of lines to keep in the log file is taken from the SADMIN 
configuration file ($SADMIN/cfg/sadmin.cfg).  
    ```bash
    SADM_MAX_LOGLINE=2000
    ```  
- You can override this value for your script by changing the value of the variable below in the 
SADMIN Section.  
    ```bash
    export SADM_MAX_LOGLINE=1000       # At end of script Trim log to 1000 Lines
    ```
- The last two lines indicate the ending date and time of the script.


## The [R]esult [C]ode [H]istory file
- Every time you run a script that's using the SADMIN Tools, there is a RCH file created or updated.
- The **RCH file are created in the SADMIN data directory '$SADMIN/dat/rch'**.
- The RCH file name is prefix by the hostname, followed by the script name and have an extension 
of '.rch'. In our example, we are on a host named 'holmes', the script name is 'helloWorld', so 
the RCH file name is 'holmes_helloWorld.rch'. 
- The SADMIN server collect every '*.rch' files that changed from every SADMIN client every 
5 minutes (via a rsync). Information included in this file will be visible from the Web interface 
and from the command line. It is also be used to trigger an alert, if it were requested.
- If you created an interactive script and you don't care about the exit code, you can disable 
usage of the RCH file.
  - In this situation, you can set variable 'SADM_USE_RCH' to 'N' in the 
[SADMIN definition section](/assets/img/sadmin_section_sh.png) of the script.  
    `export SADM_USE_RCH="N"        # Generate Entry in Result Code History file`     
  - The default maximum number of lines to keep in the '.rch' file is taken from the SADMIN 
configuration file ($SADMIN/cfg/sadmin.cfg).   
    ```SADM_MAX_RCHLINE=125```   
- You can override this default by changing 'SADM_MAX_RCLINE' variable in the SADMIN Section of your script.   
    `export SADM_MAX_RCLINE=125     # When Script End Trim rch file to 125 Lines`    
  - By default the RCH file is trim at the end of each execution (Unless 'SADM_MAX_RCLINE' is set to 0.).

**Example of a [R]esult [C]ode [H]istory file**   
![rch_file_format.png](/assets/img/files/rch_file_format.png "SADMIN rch_file_format"){: .align-center}


## A [R]esult [C]ode [H]istory file was created
- If you created an interactive script and you don't care about the exit code, you can disable usage of the RCH file.
- In this situation, you can set variable 'SADM_USE_RCH' to 'N' in the SADMIN Section of the script.  
    `export SADM_USE_RCH="Y"        # Generate Entry in Result Code History file`   
- By default the RCH file is trim at the end of each execution (Unless specified otherwise SADM_USE_RCH="N").
- The RCH file is trim to the number of line specified in $SADMIN/cfg/sadmin.cfg by the variable 'SADM_MAX_RCHLINE'.
- You can override this default by changing 'SADM_MAX_RCLINE' variable in the SADMIN Section of your script.   
    `export SADM_MAX_RCLINE=125     # When Script End Trim rch file to 125 Lines`    

    The [R]esult [C]ode [H]istory file that was created

 

## The script log file

- When a script is run that's using the SADMIN Tools, there is a log file created or updated.
- Log are created in the $SADMIN/log directory.
- The log file name is prefix by the hostname, followed by the script name and have an extension of '.log'
- In our example, we are on a host named 'holmes', the script name is 'helloWorld', so the log name is 'holmes_helloWorld.log'.
- The SADMIN server collect every log files that changed from every SADMIN client every 5 minutes (via a rsync).
- The log of a script can be cumulative or a new one can be created at each execution.
- The default in the template is set to created a new log file at each execution (SADM_LOG_APPEND="N")
- But if you want your script log to be cumulative, then set the SADM_LOG_APPEND="Y" to "Y".  
    `export SADM_LOG_APPEND="Y"     # [Y]=Append Existing Log [N]=Create New One`   
- By default the log file is trim at the end of each execution.
- The log file is trim to the number of line specified in $SADMIN/cfg/sadmin.cfg by the variable 'SADM_MAX_LOGLINE'.
- You can override this default by changing 'SADM_MAX_LOGLINE' variable in the SADMIN Section of your script.  
    `export SADM_MAX_LOGLINE=1000   # At end of script Trim log to 1000 Lines`   

### The log file file that was created  
![sadm_template_sh_30.png](/assets/img/sadm_template_sh_30.png "Log Output Example"){: .align-left}   


### RCH and log file can be viewed from the Web interface  
![sadm_template_sh_34.png](/assets/img/sadm_template_sh_34.png "Web view of example script"){: .align-left}  

### Web view of the log  
![sadm_template_sh_42.png](/assets/img/sadm_template_sh_42.png "Web view of script log"){: .align-left}  

### Web view of the RCH file   
![sadm_template_sh_38.png](/assets/img/sadm_template_sh_38.png "Web view of script rch file"){: .align-left}  


### Viewing all systems "*.rch' scripts results on the terminal  
```bash
# srch  
```
![sadm_template_sh_45.png](/assets/img/sadm_template_sh_45.png "Command line view of our scripts"){: .align-left}   

<br> 
## Controlling the script Header and Footer output

To suppress header/footer from log and screen, change "**SADM_LOG_FOOTER**" and 
"**SADM_LOG_HEADER**" variable from "Y" to "N".   
![sadm_template_sh_20.png](/assets/img/sadm_template_sh_20.png "Portion of SADMIN Section"){: .align-left}  

<br>
As you can see now the header and footer doesn't appear anymore on the screen (and in the log of the script).  
![sadm_template_sh_24.png](/assets/img/sadm_template_sh_24.png "Output with No Header & Footer"){: .align-center}  
