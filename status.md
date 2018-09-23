---
layout: default
---

## vulpine.club status

### Current status

~~This page knows of no reason why everything shouldn't be working fine.~~

There are currently intermittent performance *and availability* issues with the ~~API endpoint (the thing your browser/client talks to) and the Queue workers (the thing that handles everything else)~~ *entire vulpine.club everything*.  Mitigation is in effect.

Current production tag:
[prod-20180923-01](https://github.com/vulpineclub/mastodon/releases/tag/prod-20180923-01)

### Log

- 2018-09-23 04:00 UTC: upgrade from prod-20180918-01 to prod-20180923-01
- 2018-09-22 22:20 EDT: sidekiq queue backlogs relating to tasks hanging, with a possible bug. @rey is on it.
  - Update #1 at 2018-09-22 23:15 EDT
    - Summary: when trying to fetch https://fedi.jort.space/objects/e8314a88-d7bc-464f-a0ad-fece8292e49b it's seizing up both web workers and sidekiq workers. [#MastoAdmin thread](https://vulpine.club/@rey/100772757547660194)
    - Symptoms: sidekiq jobs are busy for a long long time with traf to fedi.jort.space (like, I've had ones at the 2+ hour mark), and searching for that status URL via API or web UI hangs.
    - Workaround: I am able to amelorate the issue by quieting then stopping the sidekiq processes via the sidekiq UI and letting them recycle, and also by doing `docker restart mastodon_web_x` to roll over the web workers.
    - Next steps: Currently we are [missing these commits in production](https://github.com/vulpineclub/mastodon/compare/a29c2e6ed8694c432c538651616e35a1c096c1df...23e7c1c765f5e500d369fcef9f020e4eb5b337d5), so I am doing a build right now.
  - Update #2 at 2018-09-22 23:30 EDT
    - Shit was hard down for a bit.  `dockerd` was swelling and eventually the oom-killer took it out, which took out everything. Everything reset itself within about five minutes.  [#VulpineClub announcement](https://vulpine.club/@rey/100772965205981928)
  - Update #3 at 2018-09-23 00:00 EDT
    - Okay, somehow, that made everything better?  I have no idea.  Anyway, I'm deploying [prod-20180923-01](https://github.com/vulpineclub/mastodon/releases/tag/prod-20180923-01) in a few moments. We'll see how that goes.
- 2018-09-18 23:30 UTC: upgrade from prod-20180912-01 to prod-20180918-01
- 2018-09-18 20:30 UTC: created this page
