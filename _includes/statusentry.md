{% capture datestring %}{{ status.date | date: "%Y-%m-%d %H:%M %z" }}{% endcapture %}
{% assign statuspage = site.statuses | where:"incident",status.incident | first %}

<li>
  <strong>{{ datestring }} // {{ status.severity }}</strong>
{% if status.incident %}
  // <a href="{{ statuspage.url }}">Details...</a>
{% endif %}

  {{ status.summary | markdownify }}

{% if status.status == 'active' %}
  <p><em>This is an active incident. Check back for more information.</em></p>
{% endif %}
</li>
