---
layout: post
title: "Should you fill your coding model's context?"
microblog: false
guid: http://rts.micro.blog/2026/08/09/should-you-fill-your-coding.html
post_id: 5966920
custom_summary: false
description: ""
date: 2026-08-09T11:07:24Z
lastmod: 2026-11-09T00:40:22Z
type: post
thumbnail: https://s3.amazonaws.com/micro.blog/thumbnails/2026/11/09/tolhurst.org/eadd9f7ce236a910d519c61c76d92f27.png
opengraph:
  title: "Richard Tolhurst Smith - Should you fill your coding model's context?"
  image: https://s3.amazonaws.com/micro.blog/opengraph/2026/08/09/5966920.png
mastodon:
  id: "117065230626324604"
  username: "tolhurst"
  hostname: "Techhub.social"
bluesky:
  id: "bafyreigngptx2vonfkxdo5fz3tjahxjeaf35lbwuofhqbclpagu5ymrlny"
  url: "at://did:plc:xs3efpengqy2qyuhpy3lpdhm/app.bsky.feed.post/3msngzygj5y2f"
  link: "https://bsky.app/profile/did:plc:xs3efpengqy2qyuhpy3lpdhm/post/3msngzygj5y2f"
  handle: "tolhurst.org"
  hostname: "bsky.social"
  did: "did:plc:xs3efpengqy2qyuhpy3lpdhm"
  document: "at://did:plc:xs3efpengqy2qyuhpy3lpdhm/site.standard.document/3msngzlbal32b"
---
It's still early days in the young field of agentic coding. We don't have many commonly agreed best practices, and those we did develop in 2025 are mostly already irrelevant in 2026. 

I am noticed one difference, which may (or may not) affect results but certainly affects token usage, and so may reflect a difference in coders who pay for their own tokens vs those who don't. 

Some coders seem to prefer very long sessions with their agents. They care about reducing token usage only to the extent that they are forced to because their context is entirely full with tokens. So they look to memory systems that can avoid storing data in context, and ways of "compacting" a session down once the context is full. I suspect they may also be the same people who love to use sub agents, because they can fire them off willy nilly without affecting the context of the main agent. (But maybe I just haven't figured out how to benefit from sub agents yet.)

I typically try to keep context under 25% full. The vast majority of tokens used in a session are the cached context tokens. Yes they are cheaper because they are cached, but they still dominate the total costs, so my costs will average a quarter of those of someone who typically works close to 100% full context. (This assumes of course that I can still achieve the same results in the same number of turns, which may not be true.)

I start a new session for almost every feature. When iterating on a feature, debugging it or adding a second similar feature it can be very tempting to maintain context, but even here I often prefer to have the agent decide which parts of the session are actually relevant and save them to a file for use by the new session. 

If I know exactly which files will need editing then I manually add those files to the context rather than have the agent grep the entire codebase. 
