---
title:          SADMIN Python library - function 'trimfile'
desc:           def trimfile(filename,nlines=500)
version:        2.2
summary:        Function used to trim a file to the desired number of lines.
updated:        2022-09-15
os:             Linux, Aix, MacOS
type:           B  # [D]oc [S]=Server only [C]=Client [B]oth
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

<a id="top_of_page"></a>
Updated: {{ page.updated }}   
{{ page.summary }} 


<h4 style="text-align:left">trimfile(filename,nlines=500)</h4>

```
Trim the file received to the number of lines indicated in the second parameter.
    - If 2nd parameter 'nlines' is omitted a value of 500 is use.
    - If 2nd parameter 'nlines' is specified and is 0, then no trim is done on the file.
    
Arguments:
    filename (str)  :   Full path of the file to trim.
    nlines (int)    :   Keep the last "nlines" lines of the file.
                        No trim is done if nlines equal 0.
Returns:
    returncode (int):   0 When command executed with success 
                        1 When error occurred (Permission Error)
```


<a id="examples"></a>
## EXAMPLE

```bash
    if ((log_footer) and (max_logline != 0)) : 
        trimfile (log_file,max_logline)                    # Trim the Script Log

```
[Back to the top](#top_of_page)

<a id="seealso"></a>
## Related function(s)

| Link to ...| Description |  
| :--- | :--- |  
| [sadm_requirements.sh]({% post_url 2019-03-21-sadm-requirements %})               | List/install required SADMIN tools packages  
