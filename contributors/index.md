---
layout: page
title: "Contributors"
comments: false
categories: [personal blog]
sharing: false
---

These lovely people have contributed a fix to my blog. If you want
to see yourself in this list, send me a pull request!

Every post in my blog has an edit link that lets you edit the blog post directly in the browser which automatically sends me a pull request.

Or [visit my repository]({{site.repo_url}}) and send me a pull
request the old fashioned way.

<ul>
{% for contributor in site.github.contributors %}
  <li>
    <img src="{{ contributor.avatar_url }}" width="32" height="32" /> <a href="{{ contributor.html_url }}">{{ contributor.login }}</a>
  </li>
{% endfor %}
</ul>