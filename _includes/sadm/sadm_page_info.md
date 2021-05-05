
<font size="3">

{% if page.type != "D" %} 
    <div>$SADMIN/bin/{{ page.title }} - Version v{{ page.version }}</div>  
{% endif %}

<div>Posted {{ page.date | date: "%Y-%m-%d" }} - Updated {{ page.updated }}</div>  

<div>Supported on {{ page.os }}</div>  

</font>  
  