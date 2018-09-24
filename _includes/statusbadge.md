{% assign outages = site.data.statuses | where:"status","active" | sort: 'date' | reverse %}
[{% if outages.size > 0 %}DEGRADED{% else %}All clear!{% endif %}]({% link status.md %})