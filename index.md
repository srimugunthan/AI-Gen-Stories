---
layout: default
---

# {{ site.title }}

{% for post in site.posts %}
- [{{ post.title }}]({{ site.baseurl }}{{ post.url }}) — {{ post.date | date: "%b %d, %Y" }}
{% endfor %}