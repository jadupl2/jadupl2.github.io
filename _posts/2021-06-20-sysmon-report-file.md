---
title:          hostname.rpt
permalink:      /hostname-rpt/
desc:           SADMIN System Monitor report file
version:        2.2
summary: |         
    This is the file generated every time the System Monitor is run.
    {: .text-justify}
updated:        2021-06-20
os:             Linux
type:           D  # [D]oc [S]=Server only [C]=Client [B]oth
categories:     [ configuration-files ] 
tags:           [ configuration-files ] 
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
<a id="top_of_page"></a>
{{ page.summary }} 
 
```bash
$ cat $SADMIN/dat/rpt/holmes.rpt
Warning;holmes;2021.06.25;10:42;linux;FILESYSTEM;Filesystem /wsadmin at 82% >= 80%;default;default
$ 

```

[Back to the top](#top_of_page)

<a id="seealso"></a>
## SEE ALSO

| Link to ...| Description |  
| :--- | :--- |  
| [How-to update SADMIN]({% post_url 2021-03-14-sadm-update %})             | How-to update to latest version of SADMIN   
| [sadmin.cfg]({% post_url 2021-04-26-sadmin-cfg %})                        | SADMIN main configuration file   
| [sadm_sysmon.pl]({% post_url 2021-06-10-sadm-sysmon %})                   | Client system monitor   
| [SysMon configuration file]({% post_url 2021-06-11-sadm-sysmon-config %}) | Client System Monitor configuration file     
| [smon]({% post_url 2021-06-15-sadm-sysmon-cli %})                         |   Allow you run SysMon and see the report file |   
| [How-to create a Slack workspace]({% post_url 2021-06-16-sadm-create-slack-workspace %}) | Create a Slack Workspace |  
| [How-to create Slack channel and App.]({% post_url 2021-06-17-sadm-create-slack-channel-and-slack-app %}) | Configure SADMIN to use Slack|  
| [How-to use SADMIN alerting system]({% post_url 2021-06-18-how-to-use-sadmin-alert %}) | Understanding SADMIN alerting system |  
| [Alert Group File]({% post_url 2021-06-19-alert-group-cfg %})                          | Alert group definition file |   
| [Slack channel file]({% post_url 2021-06-22-alert-slack-cfg %})                  |  Slack channel definition file |   




