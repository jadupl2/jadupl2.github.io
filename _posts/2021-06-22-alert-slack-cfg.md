---
title:          alert_slack.cfg
desc:           SADMIN Slack alert group definition file
version:        2.2
summary: |         
    This is the default Slack alert group definition file.
    {: .text-justify}
updated:        2021-06-22
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
# SADMIN Slack Channel file
# This file associate a SADMIN Slack Channel Name with a Slack WebHook.
#
# This file define each channel name that can be used in the 
# SADMIN Alarm Group file ($SADMIN/cfg/alert_group.cfg)
#
# Channel name used in a Slack Group MUST first be define in this file.
#
# - If the Slack Channel file ($SADMIN/cfg/slackchannel.cfg) file 
#   doesn't exist then an initial Slack Channel file is created from
#   the default Slack Channel file ($SADMIN/cfg/.slackchannel.cfg).
#
# - Blank line or line beginning with a pound sign (#) are ignored.
# - Field delimiter is a space. 
#
# FIRST COLUMN 
#   - First column of this file is the Slack Channel Name used in
#     the Slack Group file. 
#   - Default channel is 'default' - Don't delete this Channel.
#   - Don't change Slack Channel name once defined.
#   - Each name MUST be uniq and must NOT contains any space or 
#     special character.
#
# SECOND COLUMN 
#   - Second column is the Slack Web Hook obtain from the Slack Web site
#     after creating a WebHook for a specific channel.
#   - Each channel Name MUST refer to ONE Slack WebHook.
#     So ONE channel refer to ONE WebHook.
#   - There is no default channel Web Hook, you must create your own.
#
# See How-to create a Slack WebHook at https://www.sadmin.ca/www/faq.php 
# --------------------------------------------------------------------
#
# If you use Slack there MUST be a default channel (Example)
default       https://hooks.slack.com/services/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
#
sadm_info     https://hooks.slack.com/services/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
sadm_dev      https://hooks.slack.com/services/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
sadm_prod     https://hooks.slack.com/services/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
sadm_devops   https://hooks.slack.com/services/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
#

```

[Back to the top](#top_of_page)

<a id="seealso"></a>
## SEE ALSO

| Link to ...| Description |  
| :--- | :--- |  
| [SADMIN installation](/_pages/install)  | SADMIN installation page |   
| [How-to update SADMIN]({% post_url 2021-03-14-sadm-update %})             | How-to update to latest version of SADMIN   
| [sadmin.cfg]({% post_url 2021-04-26-sadmin-cfg %})                        | SADMIN main configuration file   
| [sadm_sysmon.pl]({% post_url 2021-06-10-sadm-sysmon %})                   | Client system monitor   
| [SysMon configuration file]({% post_url 2021-06-11-sadm-sysmon-config %}) | Client System Monitor configuration file     
| [smon]({% post_url 2021-06-15-sadm-sysmon-cli %})|   Allow you run SysMon and see the report file |   
| [How-to create a Slack workspace]({% post_url 2021-06-16-sadm-create-slack-workspace %}) | Create a Slack Workspace |  
| [How-to create Slack channel and App.]({% post_url 2021-06-17-sadm-create-slack-channel-and-slack-app %}) | Configure SADMIN to use Slack|  
| [How-to use SADMIN alerting system]({% post_url 2021-06-18-how-to-use-sadmin-alert %}) | Understanding SADMIN alerting system |  
| [Alert Group File]({% post_url 2021-06-19-alert-group-cfg %})                          | Alert group definition file |   
| [Slack channel file]({% post_url 2021-06-22-alert-slack-cfg %})                  |  Slack channel definition file |   

