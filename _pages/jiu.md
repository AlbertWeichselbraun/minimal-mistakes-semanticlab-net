---
layout: default
title: Jiu
---

## Jiu Techniken

<ul>
{% for j in site.jiu %}
  <li><a href="{{ site.url }}{{ site.baseurl }}{{ j.url }}">
        {{ j.title }}
      </a>
      <p class="post-excerpt">{{ j.description | truncate: 160 }}</p>
  </li>
{% endfor %}  
</ul>
