---
layout: post
title: "Should agents write comments?"
microblog: false
guid: http://rts.micro.blog/2026/08/09/should-agents-write-comments.html
post_id: 5966914
custom_summary: false
description: ""
date: 2026-08-09T10:36:01Z
lastmod: 2026-08-09T10:36:08Z
type: post
thumbnail: https://s3.amazonaws.com/micro.blog/thumbnails/2026/08/09/tolhurst.org/b14d0a0137a1e3f3964bcd1cfddb0405.png
opengraph:
  title: "Richard Tolhurst Smith - Should agents write comments?"
  image: https://s3.amazonaws.com/micro.blog/opengraph/2026/08/09/5966914.png
mastodon:
  id: "117065107171468548"
  username: "tolhurst"
  hostname: "Techhub.social"
bluesky:
  id: "bafyreiboierebvfm7tjadjf2bw6dwyyxxbuumvpb5qvaqyar2spyxtxkyi"
  url: "at://did:plc:xs3efpengqy2qyuhpy3lpdhm/app.bsky.feed.post/3msnfbtv23m2g"
  link: "https://bsky.app/profile/did:plc:xs3efpengqy2qyuhpy3lpdhm/post/3msnfbtv23m2g"
  handle: "tolhurst.org"
  hostname: "bsky.social"
  did: "did:plc:xs3efpengqy2qyuhpy3lpdhm"
  document: "at://did:plc:xs3efpengqy2qyuhpy3lpdhm/site.standard.document/3msnfbgoz4q23"
---
Most models default to writing a lot of comments: four lines of comments for one line of code is not unusual. But some people really dislike this: the system prompt of OpenCode agent tells the model not to write any comments at all!

Generally I prefer commented code, so why might you not?

1. Code should be "self-documenting" so writing comments discourages this. I think languages vary in this. For example, Java code is very verbose with long identifiers and discourages anything magical so probably shouldn't need as much commentary. But other languages are more succinct, and it's not like you can't both write clear code and also clear comments. 

2. Excessive comments make code harder to read. This is true for code you've recently written, but even then you can probably collapse the comments in your IDE. For code not in your working memory comments are useful. 

3. Out-of-date comments are worse than no comments and it's difficult to keep them up to date. This is true, but the whole point of agentic coding is you don't have to keep anything up to date; the agent does it for you. 

4. Agents like to include irrelevant details in comments, linking them to design decisions made in different modules. This is indeed a problem and it requires you to edit or delete comments during code review. 

5. Comments increase code size by a large factor, which means less code can fit in your model's context window. This is I suspect the main reason behind OpenCode's ban on comments. The counter argument is that those comments provide the agent with additional understanding. I think which side you come down on on this issue might depend on the broader issue of how you like to use context. 
