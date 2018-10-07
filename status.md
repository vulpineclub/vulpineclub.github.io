---
layout: default
title: system otterational status
permalink: /status
---

<!--
Entries are added to this page by adding them to _data/statuses.yml

Here is a full entry:

- date: 2018-09-23 02:20:00 +0000
  severity: degraded performance
  summary: rey worked a queue backlog and resource exhaustion issue caused by an edge case in the processing of certain media attachments. This problem was unique to vulpine.club.
  incident: 2018-09-23-01
  status: active

This gets rendered into:

"""
2018-09-23 02:20 +0000 // degraded performance // Details...
rey worked a queue backlog and resource exhaustion issue caused by an edge case in the processing of certain media attachments. This problem was unique to vulpine.club.

This is an active incident. Check back for more information.
"""

date: in date format, like that
severity: degraded performance, upgrade, whatever
summary: human-facing summarization
incident: if there's a long pile o' crap to read, put it in _statuses/2018-09-23-01-blahblah.md or whatever and it'll link to it
status: 'active' makes it show as an active issue
-->

<!--
Last known production tag: _data/sitedata.yml, the "production" variable
-->

{% assign statuses = site.data.statuses | sort: 'date' | reverse %}
{% assign actives = statuses | where:"status","active" %}

{% if actives.size > 0 %}
**There {% if actives.size > 1 %}are{% else %}is{% endif %} {{ actives.size }} known issue{% if actives.size > 1 %}s{% endif %}:**

<ul>
{% for status in actives %}
  {% include statusentry.md %}
{% endfor %}
</ul>

{% else %}
This page knows of no reason why everything shouldn't be working fine.
{% endif %}

<small>
Page last rendered: {{ site.time | date: "%Y-%m-%d %H:%M:%S %z" }}
<br/>
Last known production tag: [{{ site.data.sitedata.production }}](https://github.com/vulpineclub/mastodon/releases/tag/{{ site.data.sitedata.production }})
</small>

### Recent incidents

<ul>
{% for status in statuses limit:10 %}
  {% include statusentry.md %}
{% endfor %}
</ul>
