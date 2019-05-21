---
layout: page
title: running
permalink: /running/
description: Submitted European Projects.
---

### posts
<table>
{% for runpost in site.running %}
<!-- <div class="project "> -->
<tr>
    <td>
        {{ runpost.date | date: '%B %-d, %Y' }}
    </td>
    <td>
    <a href="{{ runpost.url | prepend: site.baseurl | prepend: site.url }}">
        {{ runpost.title }}
    </a>    
    </td>
</tr>  
{% endfor %}
</table>
