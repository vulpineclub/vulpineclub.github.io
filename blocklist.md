---
layout: default
title: instance blacklist
permalink: /blocklist
breadcrumb: ./
---

<!--
To Add Entries to This List,
You Should:

Add them to _data/blocks.yml in this format:


- domain: noagendasocial.com
  severity: suspend
  date: 2017-04-16
  reason: podcast dudebro brigade, no CoC, admin violations of our CoC
  link: https://vulpine.club/@rey/87813

domain, severity, and reason are REQUIRED
date and link should be omitted if unavailable
-->

{% assign blocks = site.data.blocks | sort: "date","first" %}
{% assign newest_block = blocks | last %}

{% capture blocktext %}
 {%- for block in blocks -%}
  {%- capture domaintext -%}
    <span title="{{ block.domain }}">`{{ block.domain | truncate: 23 }}`</span>
  {%- endcapture -%}

  {%- capture reasontext -%}
    {{ block.reason }}{% if block.link %}<br/><br/>[More information...]({{ block.link }}){% endif %}
  {%- endcapture -%}

  {{ domaintext }} | {{ block.severity }} | {{ block.date | default: "unknown" | date: "%Y&nbsp;%b&nbsp;%d" }} | {{ reasontext }}
 {% endfor %}
{% endcapture %}

## vulpine.club instance blocklist

- Statistics
  - Total entries: {{ blocks.size }}
  - Newest entry: {{ newest_block.date }}
- Edit history
  - [This document](https://github.com/vulpineclub/vulpineclub.github.io/commits/master/blocklist.md)
  - [Blocklist data](https://github.com/vulpineclub/vulpineclub.github.io/commits/master/_data/blocks.yml)
- Notes
  - You may need to be logged into vulpine.club to view some of the "Why" links.
  - We generally do not use external blocklists. However, [dzuk's blocklist](https://github.com/dzuk-mutant/blockchain/) contains a lot of evidence and background information.

Domain | Severity | Date | Why
-------|----------|------|-----
{{ blocktext }}

### Severity legend

<dl>
    <dt>nomedia</dt>
    <dd>
        Media files from the server are not stored and therefore not displayed. Can be coupled with the 'silence' severity.
    </dd>
    <dt>silence</dt>
    <dd>
        Accounts from the server can still be found, followed and interacted with, however, toots from the server do not appear in the public timelines, and notifications don't reach local users unless that user follows the author.
    </dd>
    <dt>suspend</dt>
    <dd>
        No content from the server is stored or displayed, no communication with the server is possible.
    </dd>
</dl>

### Common shorthand

<dl>
    <dt>asshat ratio too high</dt>
    <dd>
        This is typically used to denote an instance that is overwhelming the federated timeline with a lot of low-quality posts. This is usually a temporary condition.
    </dd>
    <dt>ban/block evasion</dt>
    <dd>
        Instances that apparently exist because the admin has been banned from too many other instances, or blocked by too many users. Generally applied to single-user or very small instances.
    </dd>
    <dt>data mining</dt>
    <dd>
        Intent to "collect all the posts" and create searchable collections for data mining, either explicit or clearly apparent. This is normally facilitated with <strong>followbots</strong>.
    </dd>
    <dt>followbots</dt>
    <dd>
        Accounts which are following a very large number of accounts across multiple instances. We will typically suspend these accounts individually when reported.
    </dd>
    <dt>freezepeach</dt>
    <dd>
        A prioritization of free speech above all. This is neither <a href="https://www.law.cornell.edu/constitution/first_amendment">required or even recommended by the US Constitution</a> nor is it condusive to healthy online communities, as it tends to create environments where shock value, drummed-up outrage, and sheer posting volume are the only ways to be heard.
    </dd>
    <dt>harassment</dt>
    <dd>
        An instance where targetted harassment is known to originate, and where the moderators turn a blind eye to it. Often related to <strong>freezepeach</strong>.
    </dd>
    <dt>illegal images</dt>
    <dd>
        Child pornography, including "simulated" child pornography. Typically, this is applied to instances known to post artwork with sexualized minors.
    </dd>
    <dt>untagged porn</dt>
    <dd>
        An instance which originates pornographic/adult/NSFW material without proper content warnings, visibility restrictions, etc.
    </dd>
</dl>
