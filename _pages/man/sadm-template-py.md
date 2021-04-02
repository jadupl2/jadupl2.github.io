---
title:          Using SADMIN Python template
layout:         single
date_created:   2021-03-16
date_updated:   2021-04-01 
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

## What you need to know to use the SADMIN tools library

The Python script template ($SADMIN/bin/sadm_template.py) include the SADMIN section and is ready to use.
The best way to learn how to use the SADMIN tools, is to create a new script as an example.
We will demonstrate further down on this page, how to use the template and what are the benefits of using it.

To create a Python script using the SADMIN tools you need to include these requirements in your code :
- The 'setup_admin()' function should appear at the beginning of your script, as in the template $SADMIN/bin/sadm_template.py.
- It create an instance of the sadmtools() class under the name 'st' ([S]admin [T]ools).

```
st = setup_sadmin()                         # Setup Var. & Load SADM Lib
```

The setup_admin() function also call the SADMIN 'sadm_start()' module/function, to initialize the environment.


```
# Start SADMIN Tools - Initialize 
st.start()                                  # Create dir. if needed, Open Log, Update RCH file..
return(st)                                  # Return Instance Obj. To Caller
```


## This is a summary of what is done by the 'st.start()' function :
- Verification and creation of the SADMIN directory structure.
- It create or append the script log (Depending on value you put in variable 'st.log_append = True').
- The starting date and time is written to the Result Code History file (See 'st.use_rch = True').
- Create the PID file, if only one copy of your script should run simultaneously ('st.multiple_exec = "N"').
- The script header is written to the log by default (see 'st.log_header = True').
- It create 3 unique temporaries files that are available to your script (st.tmp_file1, st.tmp_file2, st.tmp_file3).


You may want to modify some of the fields before the call is made to the start function (st.start()).
- You may want to change the version number of your script ('st.ver').
- Do you want a single copy of your script running at the same time ('st.multiple_exec') ?
- If you plan to use the server database, ensure that the field 'st.usedb' is set to True (Available only on SADMIN server)
- If you use the server Database, the 'st.dbsilent' field control what happen when an error occur :
- Either set to 'False' or 'True', when an error occur the error number will be returned to caller.
- Additionally, if 'st.silent' is set to False, an error message will be shown (No message when set to 'True').

- The 'st.stop(st.exit_code)' function need to be called at the end of the script (See example below).
- If the server database was used (st.usedb=True), the connection to server database will be closed.



## Another 'Hello World' example

First thing to do is to make a copy of the template Python script, into the user ($SADMIN/usr/bin) directory.
```
$ cp $SADMIN/bin/sadm_template.py $SADMIN/usr/bin/helloWorld.py
```

You should never modify the original template, always make a copy and then use the copy.
Never modify the original template directly, as it could get updated by a newer version of SADMIN.
The user directory ($SADMIN/usr) is your directory and will never be modified by the sadmin updater.

 With the editor of your choice, add the line below in the function called 'main_process(st)'.
```
st.writelog ("Hello World")
```

One of the function included in the SADMIN Python Library is "st.writelog()".
By default, it write the string it received to the screen and to the script log.
If you want to write the message to the log only, you can modify the variable "st.log_type".
```
st.log_type = 'B'             # Output goes to [S]creen [L]ogFile [B]oth
```

Let's run our script now and see the output we get.

Let's look at what happen when we ran the script.

### The Script Header
- The script header is created by the 'st.start()' function include in SADMIN Python Library.
- Every script using SADMIN library will display by default a script header.
- Unless you set the attribute 'st.log_header' to 'False' in the SADMIN Section of the script.
- st.log_header = True           # Show/Generate Header in script log (.log)
- The first line is a delimiter line consisting of eighty equal sign '='.
- The second line of the header show the name of the script, is version number and the SADMIN library version.
- You set the script version number in the SADMIN Section of the script.
- st.ver = "2.1"                 # Current Script Version
- The Library version number is available to you in a read only attribute called "set.libver".
- The third one, show the server name (FQDN) and the type of server (LINUX,AIX,DARWIN)
- The fourth line show the distribution name, it's version number and version of the kernel
- The last line is a separator line that signal the end of the header and the beginning of the script output.

#### The Script Footer
- Every script using SADMIN library, will show by default the script footer.
- Unless you set the attribute 'st.log_footer' to 'False' in the SADMIN Section of the script.
- st.log_footer = True           # Show/Generate Footer in script log (.log)
- The first line is a separator line that signal the end of the script and the beginning of the footer output.
- The second line show the exit code of the script (0=Success 1=Error).
- The third one, show the execution elapse time (HH:MM:SS).
- Next we have the name of the [R]eturn [C]ode [H]istory file and the maximum of lines to keep in it.
- The maximum number of lines to keep in the RCH file is taken from the SADMIN configuration file ($SADMIN/cfg/sadmin.cfg).
- SADM_MAX_RCHLINE=125
- You can override this value for your script, by changing the value of the attribute below in the script.
- st.cfg_max_rchline  = 125      # When Script End Trim rch file to 125 Lines
- The next line inform you if an alert will be send or not.
- The log file name is one the next line along with the maximum of lines to keep in it.
- The maximum number of lines to keep in the log file is taken from the SADMIN configuration file ($SADMIN/cfg/sadmin.cfg).
- SADM_MAX_LOGLINE=2000
- You can override this value for your script by changing the value of the attribute below in the SADMIN Section of th- script.
- st.cfg_max_logline  = 1000     # When Script End Trim log file to 1000 Lines
- The last two lines indicate the execution ending date and time and a line consisting of eighty equal sign '='- 
- A [R- sult [C]ode [H]istory file was created
- Every time you run a script that's using the SADMIN Tools, there is a RCH file created or updated.
- The RCH file is created in the SADMIN data directory '$SADMIN/dat/rch'.
- The RCH file name is prefix by the hostname, followed by the script name and have an extension of '.rch'
- In our example, we are on a host named 'holmes', the script name is 'helloWorld', so the RCH file name i- 'holmes_helloWorld.rch'.
- The SADMIN server collect every rch files that changed from every SADMIN client every 5 minutes (via a rsync).
- The information included in this file will be visible from the Web interface and on the command line.
- It could also be used to trigger an alert, if it were requested.
- If you created an interactive script and you don't care about the exit code, you can disable usage of the RCH file.
- In this situation, you can set attribute 'st.use_rch' to 'False' in the SADMIN Section of the script.
- st.use_rch = False             # Generate entry in Result Code History (.rch) 
- By default the RCH file is trim at the end of each execution (Unless specified otherwise 'st.use_rch = False').
- The RCH file is trim to the number of line specified in $SADMIN/cfg/sadmin.cfg by the variable 'SADM_MAX_RCHLINE'.
- You can override this default by changing 'st.cfg_max_rchline' attribute in the SADMIN Section of your script.
- st.cfg_max_rchline  = 125      # When Script End Trim rch file to 125 Line- 
        Example of a [R]esult [C]ode [H]istory file


### A log file was created
- When a script is run that's using the SADMIN Tools, there's a log file created or updated.
- Log are created in the $SADMIN/log directory.
- The log file name is prefix by the host name, followed by the script name and '.log' extension.
- In our example, we are on a host named 'imac', the script name is 'helloWorld', so the log name is 'imac_helloWorld.log'.
- The SADMIN server collect every updated log files from every SADMIN client every 5 minutes (via a rsync i- sadm_fetch_clients.sh).
- The log of a script can be cumulative or a new one can be created at each execution.
- The default in the template is set to created a new log file at each execution (SADM_LOG_APPEND="N")
- But if you want your script log to be cumulative, then set 'st.log.append = True'.
- st.log_append       = False    # Append Existing Log or Create New One
- By default the log file is trim at the end of each execution.
- The log file is trim to the number of line specified in $SADMIN/cfg/sadmin.cfg by the variable 'SADM_MAX_LOGLINE'.
- You can override this default by changing 'st.cfg_max_logline' attribute value in the SADMIN Section of your script.
- st.cfg_max_logline  = 1000     # When Script End Trim log file to 1000 Lines

The log file file that was created


RCH and log file can be viewed from the Web interface
Web view of our helloWorld script


Example of viewing a RCH file from the web interface


Example of a script log from the web interface


Viewing all your servers scripts results on the terminal

This option is only available on the SADMIN server.


### Controlling the script Header and Footer output
- To suppress header/footer from log and screen, change "st.log_footer" and "st.log_header" attribute to 'False'.


We can see now the header and footer doesn't appear anymore on the screen and in the log of the script.

I hope this page was useful for you. 
