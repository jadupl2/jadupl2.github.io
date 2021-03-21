---
title:          Using SADMIN Shell script template
layout:         single
date_created:   2021-03-16
date_updated:   2021-03-16 
limit:          1
paginate:       false
show_excerpts:  false
entries_layout: list
author_profile: true
tags:           slack alert scripts
categories:     alert
toc:            false
classes: wide
---

<br>
We have included 3 templates that are ready to use :  
- The [Shell script template](/_pages/man/sadm-template-sh) ($SADMIN/bin/sadm_template.sh).  
- The [Python script template](/_pages/man/sadm-template-py) ($SADMIN/bin/sadm_template.py).    
- The [SADMIN wrapper script](/_pages/man/sadm-wrapper) allow you to run existing script and benefit of the SADMIN tools ($SADMIN/bin/sadm_wrapper.sh).  
 

### What you need to know to use the SADMIN tools library.  
- The SADMIN Shell script template ($SADMIN/bin/sadm_template.sh) already include these requirements and is ready to use.  
- We will demonstrate on this page how to use this template and what are the benefits of using it.  
- The best way to learn how to use the SADMIN tools, is to create a script from the included template as an example.  

<br>
### The script template script include three things :

    The SADMIN definition section at the beginning of your script, that set script parameters and load the Shell Library.

```
#===================================================================================================
# To use the SADMIN tools and libraries, this section MUST be present near the top of your code.
# SADMIN Section - Setup SADMIN Global Variables and Load SADMIN Shell Library
#===================================================================================================

# MAKE SURE THE ENVIRONMENT 'SADMIN' IS DEFINED, IF NOT EXIT SCRIPT WITH ERROR.
if [ -z $SADMIN ] || [ ! -r "$SADMIN/lib/sadmlib_std.sh" ]          # If SADMIN EnvVar not right
    then printf "\nPlease set 'SADMIN' environment variable to the install directory."
         EE="/etc/environment" ; grep "SADMIN=" $EE >/dev/null      # SADMIN in /etc/environment
         if [ $? -eq 0 ]                                            # Yes it is 
            then export SADMIN=`grep "SADMIN=" $EE |sed 's/export //g'|awk -F= '{print $2}'`
                 printf "\n'SADMIN' Environment variable was temporarily set to ${SADMIN}."
            else exit 1                                             # No SADMIN Env. Var. Exit
         fi
fi 

# USE CONTENT OF VARIABLES BELOW, BUT DON'T CHANGE THEM (Used by SADMIN Standard Library).
export SADM_PN=${0##*/}                             # Current Script filename(with extension)
export SADM_INST=`echo "$SADM_PN" |cut -d'.' -f1`   # Current Script filename(without extension)
export SADM_TPID="$$"                               # Current Script PID
export SADM_HOSTNAME=`hostname -s`                  # Current Host name without Domain Name
export SADM_OS_TYPE=`uname -s | tr '[:lower:]' '[:upper:]'` # Return LINUX,AIX,DARWIN,SUNOS 

# USE AND CHANGE VARIABLES BELOW TO YOUR NEEDS (They influence execution of standard library).
export SADM_VER='2.8'                               # Your Current Script Version
export SADM_LOG_TYPE="B"                            # Write goes to [S]creen [L]ogFile [B]oth
export SADM_LOG_APPEND="N"                          # [Y]=Append Existing Log [N]=Create New One
export SADM_LOG_HEADER="Y"                          # [Y]=Include Log Header  [N]=No log Header
export SADM_LOG_FOOTER="Y"                          # [Y]=Include Log Footer  [N]=No log Footer
export SADM_MULTIPLE_EXEC="N"                       # Allow running multiple copy at same time ?
export SADM_USE_RCH="Y"                             # Generate Entry in Result Code History file
export SADM_DEBUG=0                                 # Debug Level - 0=NoDebug Higher=+Verbose
export SADM_TMP_FILE1=""                            # Temp File1 you can use, Libr will set name
export SADM_TMP_FILE2=""                            # Temp File2 you can use, Libr will set name
export SADM_TMP_FILE3=""                            # Temp File3 you can use, Libr will set name
export SADM_EXIT_CODE=0                             # Current Script Default Exit Return Code

. ${SADMIN}/lib/sadmlib_std.sh                      # Load Standard Shell Library Functions
export SADM_OS_NAME=$(sadm_get_osname)              # O/S in Uppercase,REDHAT,CENTOS,UBUNTU,...
export SADM_OS_VERSION=$(sadm_get_osversion)        # O/S Full Version Number  (ex: 7.6.5)
export SADM_OS_MAJORVER=$(sadm_get_osmajorversion)  # O/S Major Version Number (ex: 7)

#---------------------------------------------------------------------------------------------------
# Values of these variables are loaded from SADMIN config file ($SADMIN/cfg/sadmin.cfg file).
# They can be overridden here, on a per script basis (if needed).
#export SADM_ALERT_TYPE=1                           # 0=None 1=AlertOnErr 2=AlertOnOK 3=Always
#export SADM_ALERT_GROUP="default"                  # Alert Group to advise (alert_group.cfg)
#export SADM_MAIL_ADDR="your_email@domain.com"      # Email to send log (To override sadmin.cfg)
#export SADM_MAX_LOGLINE=500                        # When script end Trim log to 500 Lines
#export SADM_MAX_RCLINE=35                          # When script end Trim rch file to 35 Lines
#export SADM_SSH_CMD="${SADM_SSH} -qnp ${SADM_SSH_PORT} " # SSH Command to Access Server 
#===================================================================================================
```   

## The call to the 'sadm_start' function to initialize SADMIN environment.

```
        # Call SADMIN Initialization Procedure
        sadm_start                                                          # Init Env Dir & RC/Log File
        if [ $? -ne 0 ] ; then sadm_stop 1 ; exit 1 ;fi                     # Exit if Problem 
```        

    The call to the 'sadm_stop' function at the end of your script (With one parameter, '0' = Success or a non-zero value = Error).

```
# Your Main process procedure
main_process                                                        # Main Process
SADM_EXIT_CODE=$?                                                   # Save Process Return Code 

# SADMIN Closing procedure - Close/Trim log and rch file, Remove PID File, Remove TMP files ...
sadm_stop $SADM_EXIT_CODE                                           # Close/Trim Log & Del PID
exit $SADM_EXIT_CODE                                                # Exit With Global Err (0/1)
```        



### Another 'Hello World' example

    First thing to do is to make a copy of the template shell script, into the user (usr/bin) script directory, so it won't be touch by subsequent release update.
    $ cp $SADMIN/bin/sadm_template.sh $SADMIN/usr/bin/helloWorld.sh

    You should never modify the original template, always make a copy and use the copy.
    You will use it more than once and it could get overwritten when updating to a newer version of SADMIN.
    The user directory ($SADMIN/usr) is the right place to put any new script you create.
    This directory ($SADMIN/usr) will never be modified by the sadmin updater.

    To create our first 'Hello World' shell script using SADMIN tools, with the editor of your choice just add the line;
    sadm_write "Hello World\n"
    in the function called 'main_process' of your new script "helloWorld.sh".

    One of the function included in the SADMIN Shell Library is "sadm_write".
    By default, it write the string it received to the screen and to the script log.
    But you can modify this behavior, by modifying the variable "SADM_LOG_TYPE" in SADMIN section.
    export SADM_LOG_TYPE="B"             # Write goes to [S]creen [L]ogFile [B]oth


    Let's run our script now and see the output we get.

Let's look at what happen when we ran the script.
 
The Script Header

    The script header is created by the 'sadm_start' function include in SADMIN Shell Library.
    Every script using SADMIN libraries will display by default a script header.
    Unless you set the variable 'SADM_LOG_HEADER' to 'N' in the SADMIN Section of the script.
    export SADM_LOG_HEADER="N"      # [Y]=Include Log Header [N]=No log Header
    The first line is a delimiter line consisting of eighty equal sign '='.
    The second line of the header show the name of the script, is version number and the SADMIN library version.
    You set the script version number in the SADMIN Section of the script.
    export SADM_VER='1.0'           # Your Current Script Version
    The Library version number is available to you in a read only variable called "$SADM_LIB_VER".
    The third one, show the server name (FQDN) and the type of server (LINUX,AIX,DARWIN)
    The fourth line show the distribution name, it's version number and version of the kernel
    The last line is a separator line that signal the end of the header and the beginning of the script output.


 
The Script Footer

    Every script using SADMIN libraries will show by default a script footer.
    Unless you set the variable 'SADM_LOG_FOOTER' to 'N' in the SADMIN Section of the script.
    export SADM_LOG_FOOTER="N"      # [Y]=Include Log Footer [N]=No log Footer
    The first line is a separator line that signal the end of the script and the beginning of the footer output.
    The second line show the exit code of the script (0=Success 1=Error).
    The third one, show the execution time of the script (HH:MM:SS).
    The fourth line show the name of the [R]eturn [C]ode [H]istory file and the maximum of lines, you decided to have in it.
    The default for the maximum number of lines to keep in the RCH file is taken from the SADMIN configuration file ($SADMIN/cfg/sadmin.cfg).
    SADM_MAX_RCHLINE=125
    You can override this value for your script by changing the value of the variable below in the SADMIN Section of the script.
    export SADM_MAX_RCLINE=100         # When Script End Trim rch file to 125 Lines
    The next line inform you if an alert will be send or not.
    The next line show the log file name and the maximum of lines, you decided to have in it.
    The default for the maximum number of lines to keep in the log file is taken from the SADMIN configuration file ($SADMIN/cfg/sadmin.cfg).
    SADM_MAX_LOGLINE=2000
    You can override this value for your script by changing the value of the variable below in the SADMIN Section of the script.
    export SADM_MAX_LOGLINE=1000       # At end of script Trim log to 1000 Lines
    The last two lines indicate the ending date and time of the script and a final line consisting of eighty equal sign '='.

 
A [R]esult [C]ode [H]istory file was created

    Every time you run a script that's using the SADMIN Tools, there is a RCH file created or updated.
    The RCH file is created in the SADMIN data directory '$SADMIN/dat/rch'.
    The RCH file name is prefix by the hostname, followed by the script name and have an extension of '.rch'
    In our example, we are on a host named 'holmes', the script name is 'helloWorld', so the RCH file name is 'holmes_helloWorld.rch'.
    The SADMIN server collect every rch files that changed from every SADMIN client every 5 minutes (via a rsync).
    The information included in this file will be visible from the Web interface and on the command line.
    It could also be used to trigger an alert, if it were requested.
    If you created an interactive script and you don't care about the exit code, you can disable usage of the RCH file.
    In this situation, you can set variable 'SADM_USE_RCH' to 'N' in the SADMIN Section of the script.
    export SADM_USE_RCH="Y"        # Generate Entry in Result Code History file
    By default the RCH file is trim at the end of each execution (Unless specified otherwise SADM_USE_RCH="N").
    The RCH file is trim to the number of line specified in $SADMIN/cfg/sadmin.cfg by the variable 'SADM_MAX_RCHLINE'.
    You can override this default by changing 'SADM_MAX_RCLINE' variable in the SADMIN Section of your script.
    export SADM_MAX_RCLINE=125     # When Script End Trim rch file to 125 Lines

    The [R]esult [C]ode [H]istory file that was created

 
A log file was created

    When a script is run that's using the SADMIN Tools, there is a log file created or updated.
    Log are created in the $SADMIN/log directory.
    The log file name is prefix by the hostname, followed by the script name and have an extension of '.log'
    In our example, we are on a host named 'holmes', the script name is 'helloWorld', so the log name is 'holmes_helloWorld.log'.
    The SADMIN server collect every log files that changed from every SADMIN client every 5 minutes (via a rsync).
    The log of a script can be cumulative or a new one can be created at each execution.
    The default in the template is set to created a new log file at each execution (SADM_LOG_APPEND="N")
    But if you want your script log to be cumulative, then set the SADM_LOG_APPEND="Y" to "Y".
    export SADM_LOG_APPEND="Y"     # [Y]=Append Existing Log [N]=Create New One
    By default the log file is trim at the end of each execution.
    The log file is trim to the number of line specified in $SADMIN/cfg/sadmin.cfg by the variable 'SADM_MAX_LOGLINE'.
    You can override this default by changing 'SADM_MAX_LOGLINE' variable in the SADMIN Section of your script.
    export SADM_MAX_LOGLINE=1000   # At end of script Trim log to 1000 Lines

    The log file file that was created


RCH and log file can be viewed from the Web interface

    Web view of our helloWorld script


    Viewing the RCH file from the web interface


    Viewing the script log from the web interface


    Viewing all your servers scripts results on the terminal


 
Controlling the script Header and Footer output

    To suppress header/footer from log and screen, change "SADM_LOG_FOOTER" and "SADM_LOG_HEADER" variable from "Y" to "N".


    We can see now the header and footer doesn't appear anymore on the screen and in the log of the script.
    . 



Accessing the server database

    In the Shell Script template, you will also find a function that demonstrate how to access the information in the server database.
    The function is called 'process_servers' and allow you to loop to each server information of your Database.
    It actually build a list of all active server (active field set to true) and test the 'ssh' to each of the servers.
    To use it, just remove the '#' in front of the 'process_server' line.
    Running the script won't harm anything, so can run it to see it in action.



I hope this page was useful for you. 