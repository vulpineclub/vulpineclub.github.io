---
layout: default
---

## vulpine.club status

### Current status

This page knows of no reason why everything shouldn't be working fine.

Current production tag:
[prod-20180923-01](https://github.com/vulpineclub/mastodon/releases/tag/prod-20180923-01)

### Log

- 2018-09-23 04:00 UTC: upgrade from prod-20180918-01 to prod-20180923-01
- 2018-09-22 22:20 EDT to 2018-09-23 00:05 EDT: @rey worked a queue backlog and resource exhaustion issue, and is doing further monitoring/testing to identify the cause of the issue.
  - Update #1 at 2018-09-22 23:15 EDT
    - Summary: when trying to fetch https://fedi.jort.space/objects/e8314a88-d7bc-464f-a0ad-fece8292e49b it's seizing up both web workers and sidekiq workers. [#MastoAdmin thread](https://vulpine.club/@rey/100772757547660194)
    - Symptoms: sidekiq jobs are busy for a long long time with traf to fedi.jort.space (like, I've had ones at the 2+ hour mark), and searching for that status URL via API or web UI hangs.
    - Workaround: I am able to amelorate the issue by quieting then stopping the sidekiq processes via the sidekiq UI and letting them recycle, and also by doing `docker restart mastodon_web_x` to roll over the web workers.
    - Next steps: Currently we are [missing these commits in production](https://github.com/vulpineclub/mastodon/compare/a29c2e6ed8694c432c538651616e35a1c096c1df...23e7c1c765f5e500d369fcef9f020e4eb5b337d5), so I am doing a build right now.
  - Update #2 at 2018-09-22 23:30 EDT
    - Shit was hard down for a bit.  `dockerd` was swelling and eventually the oom-killer took it out, which took out everything. Everything reset itself within about five minutes.  [#VulpineClub announcement](https://vulpine.club/@rey/100772965205981928)
  - Update #3 at 2018-09-23 00:00 EDT
    - Okay, somehow, that made everything better?  I have no idea.  Anyway, I'm deploying [prod-20180923-01](https://github.com/vulpineclub/mastodon/releases/tag/prod-20180923-01) in a few moments. We'll see how that goes.
  - MONITORING at 2018-09-23 00:05 EDT: Things are holding together for right now. I'm going to do further testing, but I think the performance impacts are mitigated for now.
  - Update #4 at 2018-09-23 00:30 EDT: Dumped all active connections a couple times over the last ten minutes while I reconfigured the timeouts on nginx.  It looks like what's happening is that the status in question causes the web worker to immediately spawn ffmpeg, which... then... hangs.
```
rtucker@smithwicks:~/vulpine.club/mastodon$ docker-compose logs -t --tail=500000 web | grep 27c502fe-1bff-423f-99b2-7eff4f4368a6
web_1         | 2018-09-23T04:30:21.032433127Z [27c502fe-1bff-423f-99b2-7eff4f4368a6] [paperclip] Trying to link /tmp/8d777f385d3dfec8815d20f7496026dc20180923-29-qotnni to /tmp/8d777f385d3dfec8815d20f7496026dc20180923-29-1tatp3t.mp4
web_1         | 2018-09-23T04:30:21.039505060Z [27c502fe-1bff-423f-99b2-7eff4f4368a6] Command :: file -b --mime '/tmp/8d777f385d3dfec8815d20f7496026dc20180923-29-1tatp3t.mp4'
web_1         | 2018-09-23T04:30:21.077223859Z [27c502fe-1bff-423f-99b2-7eff4f4368a6] [AV] Running command: if command -v avprobe 2>/dev/null; then echo "true"; else echo "false"; fi
web_1         | 2018-09-23T04:30:21.083051152Z [27c502fe-1bff-423f-99b2-7eff4f4368a6] [AV] Running command: if command -v ffmpeg 2>/dev/null; then echo "true"; else echo "false"; fi
web_1         | 2018-09-23T04:30:21.100201084Z [27c502fe-1bff-423f-99b2-7eff4f4368a6] [AV] Found ["ffmpeg"], using: Ffmpeg
web_1         | 2018-09-23T04:30:21.100241350Z [27c502fe-1bff-423f-99b2-7eff4f4368a6] [AV] Running command: if command -v avprobe 2>/dev/null; then echo "true"; else echo "false"; fi
web_1         | 2018-09-23T04:30:21.102135747Z [27c502fe-1bff-423f-99b2-7eff4f4368a6] [AV] Running command: if command -v ffmpeg 2>/dev/null; then echo "true"; else echo "false"; fi
web_1         | 2018-09-23T04:30:21.125824781Z [27c502fe-1bff-423f-99b2-7eff4f4368a6] [AV] Found ["ffmpeg"], using: Ffmpeg
web_1         | 2018-09-23T04:30:21.125875741Z [27c502fe-1bff-423f-99b2-7eff4f4368a6] [AV] Running command: ffmpeg -i "/tmp/8d777f385d3dfec8815d20f7496026dc20180923-29-qotnni" 2>&1
web_1         | 2018-09-23T04:30:21.221700477Z [27c502fe-1bff-423f-99b2-7eff4f4368a6] [paperclip] [transcoder] Transocding supported file /tmp/8d777f385d3dfec8815d20f7496026dc20180923-29-qotnni
web_1         | 2018-09-23T04:30:21.221743708Z [27c502fe-1bff-423f-99b2-7eff4f4368a6] [AV] Adding output parameter ["acodec", "aac"]
web_1         | 2018-09-23T04:30:21.221750104Z [27c502fe-1bff-423f-99b2-7eff4f4368a6] [AV] Adding output parameter ["strict", "experimental"]
web_1         | 2018-09-23T04:30:21.227439541Z [27c502fe-1bff-423f-99b2-7eff4f4368a6] [AV] Adding output parameter [:filter_complex, "\"color=c=black:s=640x360,format=yuv420p[v]\""]
web_1         | 2018-09-23T04:30:21.237316553Z [27c502fe-1bff-423f-99b2-7eff4f4368a6] [AV] Adding output parameter [:map, "\"[v]\" -map 0:a"]
web_1         | 2018-09-23T04:30:21.237453958Z [27c502fe-1bff-423f-99b2-7eff4f4368a6] [AV] Adding output parameter [:threads, 2]
web_1         | 2018-09-23T04:30:21.237481490Z [27c502fe-1bff-423f-99b2-7eff4f4368a6] [AV] Adding output parameter [:vcodec, "libx264"]
web_1         | 2018-09-23T04:30:21.237487583Z [27c502fe-1bff-423f-99b2-7eff4f4368a6] [AV] Adding output parameter [:acodec, "aac"]
web_1         | 2018-09-23T04:30:21.257571879Z [27c502fe-1bff-423f-99b2-7eff4f4368a6] [AV] Adding output parameter [:movflags, "+faststart"]
web_1         | 2018-09-23T04:30:21.257596194Z [27c502fe-1bff-423f-99b2-7eff4f4368a6] [AV] Running command: ffmpeg -i "/tmp/8d777f385d3dfec8815d20f7496026dc20180923-29-qotnni" -acodec aac -strict experimental -filter_complex "color=c=black:s=640x360,format=yuv420p[v]" -map "[v]" -map 0:a -threads 2 -vcodec libx264 -acodec aac -movflags +faststart -y "/tmp/8d777f385d3dfec8815d20f7496026dc20180923-29-qotnni20180923-29-1igq0gp.mp4"
```
(ffmpeg is still running, 5 minutes later, but the web request timed out a long time ago)

- 2018-09-18 23:30 UTC: upgrade from prod-20180912-01 to prod-20180918-01
- 2018-09-18 20:30 UTC: created this page
