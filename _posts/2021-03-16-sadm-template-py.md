---
title:          Using SADMIN Python script template
permalink:      /sadm-template-py/
desc:           How-to use the Python script template
version:        2.2
updated:        2021-05-05
os:             Linux, Aix, MacOS
type:           D  # [D]oc [S]=Server only [C]=Client [B]oth
tags:           templates
categories:     templates
#
layout:         single
search:         true
author_profile: false
toc:            false
classes:        wide
sidebar:
  title:        "Documentation"
  nav:          sidebar-manpage
sadm_header_footer:     sadm/log_header_footer.md
sadm_file_rch:          sadm/sadm_rch_file.md
---


{% include sadm/sadm_page_info.md %}

## What you need to know to use the SADMIN tools library
The Python script template ($SADMIN/bin/sadm_template.py) is ready to use and it include everything 
to use the SADMIN python library. Run the template and take a look at the code.  
As an example, we will create create a new script from that template and show you what are 
the benefits of using it.
{: .text-justify}



## Another 'Hello World' example
First, make a copy of the template Python script, into the user ($SADMIN/usr/bin) directory.
```bash
$ cp $SADMIN/bin/sadm_template.py $SADMIN/usr/bin/helloWorld.py
```

You should **never modify the original template**, always make a copy and then use the copy.
The Python template supplied with SADMIN, could get updated by a newer version of SADMIN.
The **user directory ($SADMIN/usr) is your directory** and will never be updated by future version.
{: .text-justify}

 With the editor of your choice, add the line below in the function called 'main_process()'.  
```st.writelog ("Hello World")```   

![sadm_template_py_01.png](/assets/img/sadm_template_py_01.png "SADMIN Section of the template"){: .align-center}


One of the function included in the SADMIN Python module is "**st.writelog()**".
By default, it write the string it received to the screen and to the script log.
If you want to write the message to the log only, you can modify the variable "**st.log_type**".   
```st.log_type = 'B'             # Output goes to [S]creen [L]ogFile [B]oth```   

Let's run our script now and see the output we get.
![sadm_template_py_06.png](/assets/img/sadm_template_py_06.png "SADMIN Section of the template"){: .align-center}

We can divide the output of the screen in three section. We have the *Header*, the 
*script execution output* and finally the script *Footer*. Let's explore each of these sections.

{% include {{ page.sadm_header_footer }} %}

{% include {{ page.sadm_file_rch }} %}




## A log file was created
- Every time a script run that's using the SADMIN Tools, there's a log file created or updated.
- **Log are created in the $SADMIN/log directory**.
- The log file name is prefix by the host name, followed by the script name and '.log' extension.
  - In our example, we are on a host named 'imac', the script name is 'helloWorld', so the log 
name is 'imac_helloWorld.log'.
- The SADMIN server collect every updated log files from every SADMIN client every 5 minutes 
(via a rsync in sadm_fetch_clients.sh).
- A script log can be cumulative or a new one can be created at each execution. The default in 
the template is set to create a new log file at each execution.
- If you want your script log to be cumulative, then set '**st.log.append = True**'.   
    ```st.log_append = False    #   Append Existing Log```    
- At the end of each execution, the log file is trim to the number of line specified in 
$SADMIN/cfg/sadmin.cfg by the variable 'SADM_MAX_LOGLINE'.
  - You can override this default by changing '**st.cfg_max_logline**' attribute value in the 
[SADMIN definition section](/assets/img/sadmin_section_py.png) of your script.   
    ```st.cfg_max_logline  = 1000     # When Script End Trim log file to 1000 Lines```    

**Example of the log file**   
![log_format_imac.png](/assets/img/files/log_format_imac.png "SADMIN log_format"){: .align-center}  



## Log and RCH file viewed from the Web interface

**Web view of our helloWorld script**
![sadm_template_py_10.png](/assets/img/sadm_template_py_10.png "SADMIN Script Web view"){: .align-center}  


**Example of viewing a RCH file from the web interface**
![sadm_template_py_14.png](/assets/img/sadm_template_py_14.png "SADMIN RCH Web view"){: .align-center}  


**Example of a script log from the web interface**
![sadm_template_py_18.png](/assets/img/sadm_template_py_18.png "SADMIN Log Web view"){: .align-center}  


**Viewing all your servers scripts results on the terminal**  
This option is only available on the SADMIN server.  
![sadm_rch_scr_summary_01.png](/assets/img/cmdline/sadm_rch_scr_summary_01.png "SADMIN View RCH on command line"){: .align-center}  



## Suppressing the script Header and Footer
To suppress header/footer from log and screen, change "st.log_footer" and "st.log_header" attribute to 'False'.
![sadm_template_py_22.png](/assets/img/sadm_template_py_22.png "Suppress Header & Footer"){: .align-center}  

We can see now the header and footer doesn't appear anymore on the screen and in the log of the script.
![sadm_template_py_26.png](/assets/img/sadm_template_py_26.png "No more Header and Footer"){: .align-center}  



## Create a script from scratch that use SADMIN Tools
To create a Python script using the SADMIN tools you need to include these requirements in your code :
- The 'setup_admin()' function should appear at the beginning of your script, as in the template $SADMIN/bin/sadm_template.py.  

```
# -----------------------------------------------------------------------------
# SADMIN section - Setup for Global Variables and import SADMIN Python module
# -----------------------------------------------------------------------------
def setup_sadmin():

  # Load SADMIN Standard Python Library Module ($SADMIN/lib/sadmlib_std.py).
  try :
      SADM = os.environ.get('SADMIN')                      # Getting SADMIN Root Dir.
      sys.path.insert(0,os.path.join(SADM,'lib'))          # Add SADMIN to sys.path
      import sadmlib_std as sadm                           # Import SADMIN Python Libr.
  except ImportError as e:                                 # If Error importing SADMIN 
      print ("Error Importing SADMIN Module: %s " % e)     # Advise User of Error
      sys.exit(1)                                          # Go Back to O/S with Error
  
  st = sadm.sadmtools()                                    # Create SADMIN instance             

  # You can use variable below BUT DON'T CHANGE THEM - They are used by SADMIN Module.
  st.pn               = os.path.basename(sys.argv[0])      # Script name with extension
  st.inst             = os.path.basename(sys.argv[0]).split('.')[0] # Name without Ext
  st.tpid             = str(os.getpid())                   # Get Current Process ID.
  st.exit_code        = 0                                  # Script Exit Code (Use it)
  st.hostname         = socket.gethostname().split('.')[0] # Get current hostname

  # CHANGE THESE VARIABLES TO YOUR NEEDS - They influence execution of SADMIN Module.
  st.ver              = "2.1"        # Current Script Version
  st.log_type         = 'B'          # Output goes to [S]creen to [L]ogFile or [B]oth
  st.log_append       = False        # Append Existing Log(True) or Create New One(False)
  st.log_header       = True         # Show/Generate Header in script log (.log)
  st.log_footer       = True         # Show/Generate Footer in script log (.log)
  st.multiple_exec    = "N"          # Allow running multiple copy at same time ?
  st.use_rch          = True         # Generate entry in Result Code History (.rch) 
  st.debug            = 0            # Increase Verbose from 0 to 9 
  st.usedb            = True         # Open/Use Database(True) or Don't Need DB(False)
  st.dbsilent         = False        # When DB Error, False=ShowErrMsg and True=NoErrMsg 
                                     # But Error Code always returned (0=ok else error)

  # Override Default define in $SADMIN/cfg/sadmin.cfg
  #st.cfg_alert_type   = 1           # 0=NoMail 1=OnlyOnError 2=OnlyOnSuccess 3=Allways
  #st.cfg_alert_group  = "default"   # Valid Alert Group are defined in alert_group.cfg
  #st.cfg_mail_addr    = ""          # This Override Default Email Address in sadmin.cfg
  #st.cfg_cie_name     = ""          # This Override Company Name specify in sadmin.cfg
  #st.cfg_max_logline  = 500         # When Script End Trim log file to 500 Lines
  #st.cfg_max_rchline  = 35          # When Script End Trim rch file to 35 Lines
  #st.ssh_cmd = "%s -qnp %s " % (st.ssh,st.cfg_ssh_port) # SSH Command to Access Server 

 # Start SADMIN Tools - Initialize 
  st.start()                         # Init. SADMIN Env. (Create dir.,Log,RCH, Open DB..)
  return(st)                         # Return Instance Object To Caller
``` 

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


## Summary of what is done by the 'st.start()' function
- Verification and creation of the SADMIN directory structure.
- It create or append the script log (Depending on value you put in variable 'st.log_append = True').
- The starting date and time is written to the Result Code History file (See 'st.use_rch = True').
- Create the PID file, if only one copy of your script should run simultaneously ('st.multiple_exec = "N"').
- The script header is written to the log by default (see 'st.log_header = True').
- It create 3 unique temporaries files that are available to your script (st.tmp_file1, st.tmp_file2, st.tmp_file3).

You may want to modify some of the fields **before** the call is made to the start function (st.start()).
- You may want to change the version number of your script ('st.ver').
- Do you want a single copy of your script running at the same time ('st.multiple_exec') ?
- If you plan to use the server database, ensure that the field 'st.usedb' is set to True (Available only on SADMIN server)
- If you use the server Database, the 'st.dbsilent' field control what happen when an error occur :
  - Either set to 'False' or 'True', when an error occur the error number will be returned to caller.
  - Additionally, if 'st.silent' is set to False, an error message will be shown (No message when set to 'True').


## Summary of what is done by the 'st.stop()' function
- The 'st.stop(st.exit_code)' function need to be called at the end of the script (See example below).  
![sadm_template_py_30.png](/assets/img/sadm_template_py_30.png "Stop function"){: .align-center}  
- If the server database was used (st.usedb=True), the connection to server database will be closed.  



