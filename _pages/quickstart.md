---
layout: single
title: Quick Start
limit: 1
paginate: false
show_excerpts: false
entries_layout: list
author_profile: true
toc:            true
---

So you just finish [installing SADMIN tools](/_pages/install) and you want to see what it can 
bring to you. First you can take a look at the web interface at "http://yourserverIP" and you could
run the two demo scripts "[sadmlib_std_demo.sh](/libraries/sadmlib-std-demo-sh)" and 
"[sadmlib_std_demo.py](/libraries/sadmlib-std-demo-py)". This will give you an idea of what
functions you have access in our Library (sadmlib_std.sh and sadmlib_std.py) and how to use them.
You can also run our [template shell script](/templates/man/sadm-template-sh) and 
[python template](/templates/sadm-template-py), take a look at the code, they are a good starting 
point to create your next shell or Python script.
{: .text-justify}


## Meet the templates
To create your own script using the SADMIN tools, you may want to take a look at the templates, 
run them and check their code. Check our tutorial page on using the 
[shell template](/_pages/man/sadm-template-sh) for a full example.
{: .text-justify}


### Shell script template
{% highlight bash %}
$SADMIN/bin/sadm_template.sh   
{% endhighlight %} 

Running the template above, will show the kind of 
[output we get on the screen](/assets/img/cmdline/sadm_template_output_screen.png), but also 
[the log](/assets/img/cmdline/sadm_template_output_log.png) that is generated along with 
[Result Code History file (.rch)](/assets/img/cmdline/sadm_template_output_rch.png).



### Python script template
{% highlight bash %}
$SADMIN/bin/sadm_template.py   
{% endhighlight %} 

By looking at the [script output](/assets/img/cmdline/sadm_template_py_output_screen.png) you will notice that we get almost the same look, this is what we wanted, standardize the usage and the output. The Shell and the 
Python library have almost the same functions and both react the same way.
{: .text-justify}


## Create your own shell script
Make a copy of one of our template, modify it to your need and run it and see the result. 
Go an have a look at the log from the command line and from the web interface. Your script is now
part of the web interface.

{% highlight bash %}
$ cp $SADMIN/bin/sadm_template.sh $SADMIN/usr/bin/newscript.sh
$ chmod 775 $SADMIN/usr/bin/newscript.sh
$ $SADMIN/usr/bin/newscript.sh
{% endhighlight %} 


## Run existing script with the wrapper
Use the [SADMIN wrapper](/_pages/man/sadm-wrapper) to run your existing script. 
Afterward, look at the log it produced in "$SADMIN/log" and the history file in "$SADMIN/dat/rch". 
You can also go to the script section on the web interface and see the same information. The web 
interface is the central point to check your scripts logs and history file. If your script fail 
(exit with non zero value), it will appear on the monitoring page of the web interface. If you 
want it can also alert you when it fail or even it succeed, it is all up to you to decide 
(See SADM_ALERT variable).
{: .text-justify}

{% highlight bash %}
$SADMIN/bin/sadm_wrapper.sh $SADMIN/usr/bin/yourscript.sh
{% endhighlight %} 


## SADMIN libraries in action
Learn how to use SADMIN Libraries by running the demos. Running the demo will give an idea of the
functions available to you in your script and how to use them. In the script output, you see 
three columns, the first shows you how to call the function, the center column give you a brief 
description of the function and the last one give the result it returned when you ran it. 
{: .text-justify}

{% highlight bash %}
$SADMIN/bin/sadmlib_std_demo.sh 
$SADMIN/bin/sadmlib_std_demo.py
{% endhighlight %} 

- [See pdf output](/assets/pdf/sadmlib_std_demo_sh.pdf) of the bash script "[sadmlib_std_demo.sh](/libraries/sadmlib-std-demo-sh)".  
- [See pdf output](/assets/pdf/sadmlib_std_demo_py.pdf) of the Python script "[sadmlib_std_demo.py](/libraries/sadmlib-std-demo-py)".  

### Terminal Menu & Tools Library

The screen below is an example of what you can easily do with the SADMIN screen library. You can 
use it to show a menu like below, it can have up to 30 items and the item are automatically 
positioning themselves to have one or two columns. It will accept user response and validate it 
for allowed values.
{: .text-justify}

Run the following command to run the example script.
{% highlight bash %}
$ sadm_template_menus.sh
{% endhighlight %} 

![menuscreen1](/assets/img/cmdline/sadm_template_menu.png "Main Menu example")

You can accept data from the terminal, validate the content numeric, position the cursor at a 
particular line and column. The "sadm_mess()" function will show an error message to the user at 
the bottom of the screen and wait for a key to be press. 
The library include all sorts of functions that will save you time when building a user interface
the terminal.

To have a complete list of functions available in the screen library, have a look at this 
[page](/libraries/sadmlib-screen).
To use use it in within your scripts, just add the command below.
{% highlight bash %}
source $SADMIN/bin/sadmlib_screen.sh 
{% endhighlight %} 
This is it, you are now ready the use the SADMIN tool.
