---
title:          How-to remove a client
permalink:      /sadm-remove-client/
desc:           How-to remove a client using the web interface
version:        2.4
updated:        2021-05-19
os:             Linux, Aix, MacOS
type:           D  # [D]oc [S]=Server only [C]=Client [B]oth
tags:           [ how-to ] 
categories:     [ how-to ] 
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

<a id="top_of_page"></a>
## Removing a SADMIN client

On this page as an example, we will delete a SADMIN client system named 'yoda'. We will show you the
basics step to remove a client and what happen behind the scene. Removing a client from SADMIN is a 
simple process and easy to do, so make sure you delete the right system. Prior to the system 
deletion a compress backup of all client information is done in an archive folder on the SADMIN
server ($SADMIN/www/dat/archive).
{: .text-justify} 

<a id="step1"></a>
## Remove a SADMIN client with the web interface  
To remove a client from the SADMIN server inventory, _click on "Server"_ in the "CRUD Operations" 
([C]reate [R]ead [U]pdate [D]elete) section at the bottom left of the page.
{: .text-justify} 

![Remove SADMIN client](/assets/img/sadm_add_client/crud_operations.png){: .align-center}  

You will be directed to a page that list all your actual SADMIN clients. With this view you can 
"Create", "Read", "Update" and "Delete" client to the server database. To delete a client from  
SADMIN inventory, _simply press the "Delete" button_ located on the same line of the client you 
wish to delete.
{: .text-justify} 

![Press "Delete" Button](/assets/img/sadm_delete_client/delete_button.png){: .align-center}  

The page below will then appear and you only need to confirm or cancel your choice. If you still 
want to delete the client from the database inventory, then press the "Delete" button. If you don't 
want to delete this system, press the "Cancel" button.
{: .text-justify} 

![Delete System Screen](/assets/img/sadm_delete_client/delete_system.png){: .align-center}  

A final confirmation will be asked, you to make sure that you really want to delete this system.

![Final Delete Confirmation](/assets/img/sadm_delete_client/delete_confirmation.png){: .align-center}  

[Back to the top](#top_of_page)



## What happen when a client is deleted 


This is the directory of the server 'yoda' prior to the deletion of this system on the SADMIN server.
```bash
$ cd $SADMIN/www/dat/yoda
$ /opt/sadmin/www/dat/yoda $ ls -l
total 24
drwxrwxr-x 2 apache apache 4096 May 20 09:45 cfg
drwxrwxr-x 2 apache apache 4096 May 20 02:13 dr
-rw-rw-r-- 1 apache apache   20 May 20 05:06 environment
drwxrwxr-x 2 sadmin sadmin 4096 May 16 00:33 log
drwxrwxr-x 2 apache apache 4096 May 20 02:15 nmon
drwxrwxr-x 2 sadmin sadmin 4096 May 20 02:13 rch
drwxrwxr-x 2 sadmin sadmin   21 May 20 09:45 rpt
```

Once we press the final confirmation, a backup of the client directory on the SADMIN server is done
to an archive directory ($SADMIN/www/dat/archive). If you ever need to have access to some 
information about that server, you can still access it. Then system directory 
($SADMIN/www/dat/hostname) is deleted. 
{: .text-justify} 

```bash
$ cd $SADMIN/www/dat/archive
/sadmin/www/dat $ ls -l yoda.tgz 
-rw-r--r-- 1 apache apache 4879879 May 20 09:56 yoda.tgz
```


{% include {{ site.section_author      }} %}

{% include {{ site.section_copyright   }} %}


<a id="seealso"></a>
## SEE ALSO

[How-to Add a client]({% post_url 2021-04-11-web-add-client %}) - How-to add a client to SADMIN inventory