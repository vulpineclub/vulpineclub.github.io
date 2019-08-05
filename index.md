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

## Supporting Vulpine Club

- [One-time Credit Card payments](https://owo-group.square.site/product/vulpineclub/5) via the [OwO Group LLC](https://owo-group.square.site/) store
- [Patreon page](https://www.patreon.com/vulpineclub) - note that the rewards aren't really being rewarded right now, sorry
- ACH, TransferWise, wire transfer, etc: Contact [@rey@vulpine.club](https://vulpine.club/@rey) for account information

## Information for Members

System status: {%- include statusbadge.md %}

- [Blocked Instances list]({% link blocklist.md %}) - last updated: {{ newest_block.date }}
- [Custom Emoji list](https://emojos.in/vulpine.club) (from emojos.in)
  - Custom emoji contributions are welcome!  E-mail to `admins` at `vulpine.club`, be sure to mention who you are and what you'd like the shortcode to be :)
    - PNG format, 50 KB maximum
    - Please package multiple emoji into a .tar.gz file
        - Filename format: `shortcode.png` -> `:shortcode:` (e.g. `heart_trans.png` would be added as `:heart_trans:`)
        - Please prefix the filenames with something unique to avoid namespace conflicts and to aid sorting (e.g. `:rey_smirk:`)
- [Financial Information]({% link financial/index.md %})
- [Local Features]({% link features/index.md %})
- Policies
  - [Age Policy]({%link policy/age-policy.md %})

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
- Operations
  - [Operations Home]({% link operations/index.md %})

![fox sketch]({{ '/assets/images/foxsketch.png' | relative_url }})
