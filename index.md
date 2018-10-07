---
layout: default
---

{% assign blocks = site.data.blocks | sort: "date","first" %}
{% assign newest_block = blocks | last %}

# Vulpine Club Documentation Portal

Welcome to the Vulpine Club documentation portal!

This is a collection of various information about the vulpine.club project, mostly from an operational perspective. If you have any comments/suggestions, please feel free to hit up our [issues list on GitHub](https://github.com/vulpineclub/vulpineclub.github.io/issues) or send a DM to [@rey@vulpine.club](https://vulpine.club/@rey).

## Connecting to the Vulpine Club

- [vulpine.club main page](https://vulpine.club/)
- Alternate links:
  [0.vulpine.club](https://0.vulpine.club/), [1.vulpine.club](https://1.vulpine.club/), [2.vulpine.club](https://2.vulpine.club/), [3.vulpine.club](https://3.vulpine.club/)
  <br/>
  <em>Each of these creates its own login session, separate from the other links. This is useful for logging into multiple accounts simultaneously, e.g. a main account and a lewd account.</em>

## Information for Members

- System status: {%- include statusbadge.md %}
- [Blocked Instances list]({% link blocklist.md %}) - last updated: {{ newest_block.date }}
- [Custom Emoji list](https://emojos.in/vulpine.club) (from emojos.in)
- [Financial Information]({% link financial/index.md %})
- [Local Features]({% link features/index.md %})

## Information for Admins

- Development
  - Fork health
    - [CircleCI status](https://circleci.com/gh/vulpineclub)
    - inbound from glitchsoc: [glitch-soc:master -> vulpineclub:master-glitchsoc](https://github.com/vulpineclub/mastodon/compare/master-glitchsoc...glitch-soc:master)
    - glitchsoc->master merge queue: [vulpineclub:master-glitchsoc -> vulpineclub:master](https://github.com/vulpineclub/mastodon/compare/master...vulpineclub:master-glitchsoc)
    - production->master merge queue: [vulpineclub:production -> vulpineclub:master](https://github.com/vulpineclub/mastodon/compare/master...vulpineclub:production)
    - vulpineclub local commits: [vulpineclub:master -> vulpineclub:master-glitchsoc](https://github.com/vulpineclub/mastodon/compare/master-glitchsoc...vulpineclub:master)
  - Build automation
    - [vulpineclub:master -> vulpineclub:production](https://github.com/vulpineclub/mastodon/compare/production...vulpineclub:master)
    - Deployments via the [production branch](https://github.com/vulpineclub/mastodon/tree/production) are [tagged with `prod-*` tags](https://github.com/vulpineclub/mastodon/tags)
    - [Docker Hub builds](https://hub.docker.com/r/vulpineclub/mastodon/builds/)

![fox sketch](/img/foxsketch.png)
