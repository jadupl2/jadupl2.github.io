---
title:          sadmlib_screen.sh
desc:           SADMIN screen oriented library
version:        2.2
updated:        2021-05-09
os:             Linux, Aix, MacOS
type:           D  # [D]oc [S]=Server only [C]=Client [B]oth
tags:           [ libraries ] 
categories:     [ libraries ] 
#
layout:         single
search:         true
author_profile: false
toc:            true
classes:        wide
sidebar:
  title:        "Documentation"
  nav:          sidebar-manpage
---

{% include sadm/sadm_page_info.md %}
<br>

This library include all the necessary components to build and display a menu of your choice and 
to accept the choice of the user and return that choice to the caller. It was used to build our
SADMIN Menu (sadm), to have an overview of what this library can help you to do just type 'sadm' at
the prompt.
{: .text-justify} 

![Menu template](/assets/img/sadm_template_menu.png){: .align-center}  

## sadm_accept_choice() 
The function accept one parameter and it's the number of item in the menu (maximum number to accept as a valid choice). Cursor is positioned on line 22, at the right of "Choice ?". Value entered MUST be numeric, unless you press "Q" or "q" to exit the menu. 
If a valid number was entered it is returned to the caller. If user press the "Q' or "q" then a value of 99 is returned.
```bash
sadm_accept_choice $s_count
choice=$?
if [ $choice -eq 99 ] 
    then echo "User have choose the [Q]uit option" 
    else echo "User have choose the menu item no.${choice}."
fi    
```


## sadm_accept_data() 
This function is used to accept data input from the user (using the keyboard). The input data is 
returned in the Global Variable $WDATA.

This function need to receive 5 parameters :
> Param #1 = Line number to accept data  
> Param #2 = Cursor position on the line  
> Param #3 = Number of Character to accept  
> Param #4 = Type of data to accept (A=AlphaNumeric N=Numeric)  
> Param #5 = Value of field just entered ("NULL"  = No Default)  
```
sadm_accept_data 04 41 25 A $RPM
```

## sadm_ask_password()
I used this function to generate a password, that I would give to my customer when they need to 
used an item in the menu that would require sysadmin privilege and that it need assistance on the 
phone. So they couldn't used it without calling and the beauty of this is that the password change 
every minute. The password generated is based on a simple formula that used the date and time, so 
it change every minute, so if the user try to use the same password later on, it won't work.
The password is asked with no echo while it is type, if the password match a value of '0' is 
returned to the caller else a '1' is returned. The password is asked on line 23 and is prefix by 
the text "Please enter the SADMIN password ...  ? ".
{: .text-justify} 
The formula used is :   
    - Take the date and time in the format 'ddmmyyHHMM'.  
      - Example for the 10 May 2021 at 13:02 the value would be 1005211302.  
    - Divide result by 824 (0101211302 / 824 = 1219916).  
    - The password would be "1219916".  
 
**Example:**
```bash
sadm_ask_password
if [ $? -ne 0 ] 
    then echo "[ ERROR ] Invalid password" 
    else echo "[OK] Valid password"
fi
```
![sadm_ask_password Example](/assets/img/sadmlib_screen/sadmlib_screen_sadm_ask_password.png){: .align-center}  


## sadm_display_heading()
This function clear the screen and display the menu heading on line one and two of the screen. It 
accept two parameters, the first one is the title you want to give to your menu and the second is 
the version number that is displayed on the right of the second line.   
On the first line there is the system hostname ($(sadm_get_fqdn)), the menu title centered ($1) and 
then on the right the current date and time. On the second line, we have the operating system name, 
followed by it version, the centered company name and completely at the right the version number 
that was received ($2).
{: .text-justify}  
**Example:**
```bash
sadm_display_heading "Your Menu Heading Here" "$SADM_VER" 
```
![Menu Heading Lines](/assets/img/sadmlib_screen/sadmlib_screen_heading.png){: .align-center}  





## sadm_display_menu()       
This function display the array of menu item in one or two columns depending on the size of array 
received and accept the choice number selected (or Q|q to Quit). The array must not contain more 
than 30 items. The menu is automatically formatted based on the number of items to displayed in 
the menu. Menu will be displayed between line 4 and 20, menu with less than 9 items will be 
displayed in one column and with more than 8 will be shown in a two column fashion.
{: .text-justify}  

- Function return the item number selected (between 1 and the number of item in array).
- Function return 98 if the number of item in the menu array is less than one or greater than 30.
- Function return 99 if the choice selected was 'Q' or 'q' for quit.

**Example:**
```bash
# Display Main Menu     
while :                                                        # loop until Q|q is press
   do
   sadm_display_heading "Filesystem Menu" "$SADM_VER"          # Std SADMIN Menu Heading
   menu_array=("Create a filesystem" \                         # Put Items 1 in menu array
            "Increase a filesystem" \                          # Put Items 2 in menu array
            "Delete a filesystem" \                            # Put Items 3 in menu array
            "Check a filesystem" )                             # Put Items 4 in menu array
   sadm_display_menu "${menu_array[@]}"                        # Display menu Array
   sadm_choice=$?                                              # Choice is returned in $?
   case $sadm_choice   in                                            
        1) sadm_mess "You selected to create a filesystem."
           ;;
        2) sadm_mess "You selected to increase a filesystem.        
           ;;
        3) sadm_mess "You selected to delete a filesystem."
           ;;
        4) sadm_mess "You selected to check a filesystem."
           ;;
       99) # Option Quit -                                     # 99 = [Q],[q] was pressed
           break                                               # Break out of the loop
           ;;
        *) # Invalid Option #                                  # If an invalid key press
           sadm_mess "Invalid option ($sadm_choice)."          # Message to user
           ;;
    esac
    done
``` 



## sadm_display_message()   
This function clear the screen starting on line 23 and then display the message received ($1) in 
'bold' on line 23 position 1. This function always return a value of 0. 
{: .text-justify} 
**Example:**  
```bash
sadm_display_message "Processing have just started."   # Advise user
```




## sadm_mess()              
I use this function, when I want to attract user attention or to display an error message. The
function display the message received ($1) on line 22 position 1 and "Press [ENTER] to continue" 
on line 23, it then wait for user to press [ENTER] to continue. When the user press [ENTER], then 
the line 22 and 23 are cleared.
{: .text-justify} 
**Example:**  
```bash
sadm_mess "Filesystem /sadminv2 doesn't exist"
```
![sadm_mess Example](/assets/img/sadmlib_screen/sadmlib_screen_sadm_mess.png){: .align-center}  



## sadm_messok()
Use this function to ask the user a question and return to the caller when he respond by 
'Y|y' or 'N|n'. You specify the line number ($1), the cursor position on the line ($2) and the 
question to ask ($3). The question is displayed with " [y,n] ? " appended to it. If the user
responded with a 'Y' or a 'y', then '1' is returned to the caller. If the user responded with 
a 'N' or a 'n', then '0' is returned to the caller. No other value is accepted.
{: .text-justify} 
**Example:**  
```bash
sadm_messok 22 01 "Do you want to increase /history filesystem by 1 MB"
if [ $? -eq 1 ] 
    then echo "User responded yes to the question." 
    else echo "User responded no to the question."
fi
```
![sadm_messok Example](/assets/img/sadmlib_screen/sadmlib_screen_sadm_messok.png){: .align-center}  





## sadm_pager()  
This function display file received ($2) on a page by page basis. The first parameter ($1) is the 
title we want to appear on the heading line. The third parameter specify the number of lines we
want to show per page. On line 22 there are options that allow you to move in the document, you can
press [N] to view the next page, [P] to move back to previous page, [Q] to quit the viewer or you
can enter the page number you want to see. 
{: .text-justify} 
**Example:**   
```bash
rpm -qi xrdp > $SADM_TMP_FILE1
sadm_pager "Display xrdp Package Information" "$SADM_TMP_FILE1" 17   
```
![File pager example](/assets/img/sadmlib_screen/sadmlib_screen_pager.png){: .align-center}  






## sadm_print_status()  
The function accept two parameters, the first one is the status and it should be "ok", "error" or 
"warning" and the second parameters is the message you want to display at the right of the first. 
Each of the status received will be shown in specific color and is placed between green bold 
bracket. The first parameter got to be one of the three possibilities below, unless it will be 
show in magenta. Message are display followed by a new line (NL).
{: .text-justify} 

| First parameter | second parameter | Output to the screen |  
| :--- | :--- | :--- |
| "ok","OK","Ok" | Will be shown in green.| [OK] Message |
| "ERROR","Error","error" | Will show in red.| [ERROR] Message |
| "Warning","WARNING","warning" | Will show in yellow.| [WARNING] Message |
| Other | Will show in magenta. | [OTHER] Message |]

**Example:**   
![Print Status Example](/assets/img/sadmlib_screen/sadmlib_screen_print_status.png){: .align-center}  





## sadm_show_menuitem() 
Maybe I shouldn't have put this function here, because I don't see usability outside the library 
context, but feel free to use it. In this library it is used to display each item on a menu.   
Function accept 4 parameters :  
 1 = LineNumber (1,24)    
 2 = Column(1,80)    
 3 = MenuItemNo   
 4 = MenuItemDesc  
{: .text-justify}   
**Example:**    
```bash
sadm_show_menuitem $wline $wrow "$menu_no" "$menu_item"  
```





## sadm_writexy()   
This function is use to display text message at the specified line and position on the screen. 
As all the functions in this library, it is working under Linux, Aix and MacOS. This function is 
by a majority of functions in this library. The first parameter is the line number, the second the
position on the line and finally the text to display.
{: .text-justify} 
**Example:**   
```bash
sadm_writexy 24 1 "message"
```




<a id="seealso"></a>
## SEE ALSO

[sadmlib_std.sh ]({% post_url 2021-04-07-sadmlib-std-sh %}) - SADMIN standard shell library  
[sadmlib_std.py ]({% post_url 2021-04-07-sadmlib-std-py %}) - SADMIN standard python library  
[sadmlib_std_demo.sh]({% post_url 2019-10-12-sadmlib-std-demo-sh %}) - SADMIN shell library functions demo   
[sadmlib_std_demo.py]({% post_url 2019-10-12-sadmlib-std-demo-py %}) - SADMIN python library functions demo  