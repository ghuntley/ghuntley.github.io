---
layout: page
title: Blog Archives
permalink: /archive/
---

<div class="archives" itemscope itemtype="http://schema.org/Blog">
{% for post in site.posts reverse %}
{% unless post.draft %}
{% if post.layout == 'post' %}
	{% include archive_post.html %}
{% endif %}
{% endunless %}
{% endfor %}
  </ul>
</div>
