---
layout: default
---

## vulpine.club status

### Current status

~~This page knows of no reason why everything shouldn't be working fine.~~

There are currently intermittent performance issues with the API endpoint (the thing your browser/client talks to) and the Queue workers (the thing that handles everything else).  Mitigation is in effect.

Current production tag:
[prod-20180918-01](https://github.com/vulpineclub/mastodon/releases/tag/prod-20180918-01)

### Log

- 2018-09-22 22:20 EDT: sidekiq queue backlogs relating to tasks hanging, with a possible bug. @rey is on it.
- 2018-09-18 23:30 UTC: upgrade from prod-20180912-01 to prod-20180918-01
- 2018-09-18 20:30 UTC: created this page
