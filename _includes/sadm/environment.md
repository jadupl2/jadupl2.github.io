<a id="environment"></a>
## ENVIRONMENT
- The **"$SADMIN"** environment variable must be defined and contains the root directory of the 
SADMIN tools (normally /opt/sadmin). It should be already done, the setup script have updated 
the '[/etc/profile.d/sadmin.sh](/assets/img/files/etc_profile_d_sadmin_sh.png)' and the 
'[/etc/environment](/assets/img/files/etc_environment.png)' files.  
- The [SADMIN configuration file]({% post_url 2021-04-26-sadmin-cfg %}), 
is needed and loaded in memory at the beginning of every scripts. This file should already exist 
and contains your SADMIN configuration and preference setting.
- For Shell script the [Shell Library]({% post_url 2021-04-07-sadmlib-std-sh %}) is used and for
Python script the [Python Library]({% post_url 2021-04-07-sadmlib-std-py %}) is used.  