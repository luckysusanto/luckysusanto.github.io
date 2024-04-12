---
layout: archive
title: "Publications"
permalink: /publications/
author_profile: true
---

{% if author.googlescholar %}
  You can also find my articles on <u><a href="{{author.googlescholar}}">my Google Scholar profile</a>.</u>
{% endif %}

{% include base_path %}

{% for post in site.publications %}
  {% unless post.title contains 'Project'%}
    {% include archive-single.html %}
{% endfor %}

{% for post in site.publications %}
  {% if post.title contains 'Project'%}
    {% include archive-single.html %}
{% endfor %}