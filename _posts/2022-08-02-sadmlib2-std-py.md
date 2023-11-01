---
title:          SADMIN Python Library v2 - sadmlib2_std.py
permalink:      /sadmlib2-std-py/
desc:           SADMIN standard python library v2
updated:        2022-09-16
version:        4.25
os:             Linux, MacOS
type:           D  # [D]oc [S]=Server only [C]=Client [B]oth
tags:           [ libraries ] 
categories:     [ libraries ] 
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

### Documentation of each functions in the library   

If you are not already familiar with our Python library, you may want to read [how-to use the SADMIN Python Library]({% post_url 2021-03-16-sadm-template-py %}).


| Function Call |   Description |  Return value example |   
| :---  | :--- | :---  |  
| check_requirements()              | Check/Set path of require cmd (False if some missing)     | True or False |
| date_to_epoch(epoch_time)         | Return date based on the Epoch time received              | YYYY.MM.DD HH:MM:SS|
| dbclose()                         | Close SADMIN database (return (0)=Success (1)=Error)      | 0 |
| dbconnect()                       | Connect to SADMIN database (return (0)=Success (1)=Error) | 0 |
| elapse_time(end,start)            | Return elapse time between end (YYYY.MM.DD HH:MM:SS) & start | 10:20:40 |
|                                   | End date MUST be greater than start date                  | |
|                                   | Elapse time is return in a string format 'HH:MM:SS'       | |
| epoch_to_date(wepoch)             | Return date as a string based on the epoch time received  | YYYY.MM.DD HH:MM:SS |
| get_arch()                        | Get current system architecture                           | x86_64 |
| get_domainname()                  | Return current host domain name                           | batcave.com |
| get_epoch_time()                  | Return current epoch time as an integer                   | 1621263948 |
| get_fqdn()                        | Return fully qualified domain dame of current system      | batserver.batcave.com |
| get_host_ip()                     | Return to main IP address of current system               | 192.168.1.12 |
| get_kernel_bitmode()              | Return kernel bit mode (32 or 64)                         | 64 |
| get_kernel_version()              | Return kernel running version                             | 5.8.0-53-generic |
| get_oscodename()                  | Return the O/S project code name                          | focal |
| get_osmajorversion()              | Return the O/S distribution major version number          | 20 |
| get_osminorversion()              | Return the O/S distribution minor version number          | 04 |
| get_osname()                      | Return the O/S name in uppercase                          | UBUNTU |
| get_ostype()                      | Return the O/S type (LINUX,AIX,DARWIN,...) in uppercase   | LINUX |
| get_osversion()                   | Return the O/S distribution version number                | 20.04 |
| get_packagetype())                | Return the O/S main package format (rpm,deb,lpp,dmg)      | deb |
| get_release()                     | Return SADMIN release version number                      | 1.3.3 |
| get_serial()                      | Return CPU serial number                                  | BJSV942 |
| load_config_file(sadmin_file)     | Load SADMIN config file & set global variables accordingly| |
| locate_command(cmd)               | Check command if available (Return cmd Path, or blank)    | |
| oscommand(command)                | Execute o/s cmd received, return(returncode,stdout,stderr)| |
| show_version()                    | Called when '-v --version' command line argument is used  | |
| silentremove(filename)            | Remove file name received - no error msg - even if failed | |
| start()                           | Make sure dir. exist, init log,rch,pid, chk multiple exec | abort if fail |
| stop(return_code)                 | Write footer to log,rch, del pid, close db, trim log,rch  | |
| [trimfile(filename,nlines=500)]({% post_url 2022-09-15-lib-trim-py %}) | Trim file received to number of lines specified(500 default) | 0 |
| writelog(msg,stype="normal")      | Write message to log File, Screen or Both (st.log_type)   | |





{% include {{ site.section_environment }} %}

{% include {{ site.section_exitcode    }} %}

{% include {{ site.section_author      }} %}

{% include {{ site.section_copyright   }} %}


<a id="seealso"></a>
## SEE ALSO

[sadm_template.py]({% post_url 2021-03-16-sadm-template-py %}) - Using SADMIN Python script template    
[sadmlib_std_demo.py]({% post_url 2019-10-12-sadmlib-std-demo-py %}) - SADMIN Python Library Functions Demo  


