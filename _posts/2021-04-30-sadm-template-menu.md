---
title:          sadm_template_menu.sh
desc:           Using SADMIN shell menu template
version:        1.4
date:           2021-04-30
updated:        2021-04-32
os:             Linux, Aix, MacOS
tags:           [ templates ]
categories:     [ templates ] 
#
layout:         single
search:         true
author_profile: false
toc:            false
classes:        wide
sidebar:
  title: "Documentation"
  nav: sidebar-manpage
---

<font size="3">
<div>$SADMIN/bin/{{ page.title }}</div>
<div>Version v{{ page.version }} - Updated {{ page.updated }}</div>
<div>Run on {{ page.os }}</div>
</font>


<a id="name"></a>
## NAME
**{{ page.title }}** - *{{ page.desc }}*   


<a id="synopsis"></a>
## SYNOPSIS

```bash
{{ page.title }} [ -d 0-9 ] [ -h ] [ -v ]
```


<a id="description"></a>
## DESCRIPTION

The best way to become familiar the menu builder, is to run the "sadm_template_menu.sh" script.
  {: .text-justify}  

```$ sudo $SADMIN/bin/sadm_template_menus.sh```

![Menu template](/assets/img/sadm_template_menu.png){: .align-center}  

<a id="examples"></a>
## EXAMPLE
sadm_template_menu.png
Here is some portion of the code in "sadm_template_menu.sh", you want to modify to create your own menu.

```bash
    # Display Main Menu     
        while :
            do
            sadm_display_heading "Your Menu Heading Here"               # Std SADMIN Menu Heading
            menu_array=("Your Menu Item 1" "Your Menu Item 2" "Your Menu Item 3" "Your Menu Item 4" )             
            sadm_display_menu "${menu_array[@]}"                        # Display menu Array
            sadm_choice=$?                                              # Choice is returned in $?
            case $sadm_choice   in                                            
                1) sadm_mess "You press choice number $sadm_choice"
                ;;
                2) sadm_mess "You press choice number $sadm_choice"
                ;;
                3) sadm_mess "You press choice number $sadm_choice"
                ;;
                4) sadm_mess "You press choice number $sadm_choice"
                ;;
            99) # Option Quit -                                         # 99 = [Q],[q] was pressed
                break                                                   # Break out of the loop
                ;;
                *) # Invalid Option #                                   # If an invalid key press
                sadm_mess "Invalid option"                              # Message to user
                ;;
            esac
            done
```


{% include {{ site.section_options     }} %}

{% include {{ site.section_environment }} %}

{% include {{ site.section_exitcode    }} %}

{% include {{ site.section_author      }} %}

{% include {{ site.section_copyright   }} %}


<a id="seealso"></a>
## SEE ALSO


