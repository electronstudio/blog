---
layout: post
title: "Thoughts on Go"
microblog: false
guid: http://rts.micro.blog/2026/03/10/thoughts-on-go.html
post_id: 5784077
custom_summary: false
description: ""
date: 2026-03-10T10:32:00Z
lastmod: 2026-06-21T11:28:40Z
type: post
categories:
- "posts"
thumbnail: https://s3.amazonaws.com/micro.blog/thumbnails/2026/06/18/tolhurst.org/c89e0154f34fa2c6c5f0edc84d8c0a5d.png
opengraph:
  title: "Richard Tolhurst Smith - Thoughts on Go"
  image: https://s3.amazonaws.com/micro.blog/opengraph/2026/03/10/5784077.png
mastodon:
  id: "116204191273603526"
  username: "tolhurst"
  hostname: "Techhub.social"
bluesky:
  id: "bafyreigitglpnqe6evyhofg7h4eqr24r6hvesik4cjgz2o4ge4bntbc7dy"
  url: "at://did:plc:xs3efpengqy2qyuhpy3lpdhm/app.bsky.feed.post/3mgp2x5kqfy27"
  link: "https://bsky.app/profile/did:plc:xs3efpengqy2qyuhpy3lpdhm/post/3mgp2x5kqfy27"
  handle: "tolhurst.org"
  hostname: "bsky.social"
  did: "did:plc:xs3efpengqy2qyuhpy3lpdhm"
---
Go is strange, for a mainstream language. If it didn't have the pedigree of being designed by the famous guys from Bell Labs and the marketing of Google behind I doubt it would have even made it to mainstream status. 

No one seems to love Go. C programmers can't stand that it has managed memory and prefer Zig or Odin. Java programmers don't want to give up their (safe, portable, fast) VM for a native solution that doesn't particularly prioritise optimisation and is not much faster. C++ programmers find the feature set limited, and if they are going to limit themselves then they will only do it for the absolute safety provided by Rust. 

Some people acknowledge that when they used it for projects in the area for which Google designed it - highly concurrent applications written by inexperienced coders - it was the optimal choice. But they still don't use it by preference. 

Go is perhaps best viewed as an experiment in finding the limit of how much you can remove and yet still be left with a productive language. (They slightly revised their initial opinions when they added generics, but they've never attempted to bolt on the mass of functional paradigm stuff that Java, Python and C++ all have.)

Go is readable in the same way that a good imperative style statically typed Python program is, with the advantage over Python that this style is enforced by the language. 

It has pointers, but they are garbage collected automatically. It has exceptions but the standard library prefers to return explicit error tuples that you check immediately at the call site (a little like option types).  There's no null checking, but null errors are minimised by preferring value types over pointers and allowing method calls to be defined for some null objects. 

Null is called nil, perhaps to emphasise it should be treated as a zero value rather than absence of value. There is one confusing point that there are two different kinds of nil, and they aren't equal. [Because there are two kinds of types, concrete types and interface types. Interface type objects contain a record of the concrete type alongside the object so allow runtime polymorphism. ]

It's statically typed but has structural typing, which feels a bit like when a dynamic language has duck typing. Typescript is the only other mainstream language I'm aware of with this. 

Concurrency is done with "goroutines" which look like coroutines but are actually lightweight threads and are part of the language, not the library. Built-in channels, mutexes and semaphores make them easier to reason about than threads. It's a "one true way" approach to concurrency that may not be optimal for every situation, but provides sufficient features for most yet few enough that complexity is minimised.
