---
layout: post
title: "An OS for a PowerPC Macintosh"
microblog: false
guid: http://rts.micro.blog/2026/01/22/an-os-for-a-powerpc.html
post_id: 5727312
custom_summary: false
description: ""
date: 2026-01-22T19:14:55Z
lastmod: 2026-03-10T09:32:32Z
type: post
thumbnail: https://s3.amazonaws.com/micro.blog/thumbnails/2026/03/10/tolhurst.org/98fbc928c38e2ecc311630aa96ea38ac.png
opengraph:
  title: "Richard Tolhurst Smith - An OS for a PowerPC Macintosh"
  image: https://s3.amazonaws.com/micro.blog/opengraph/2026/03/10/5727312.png
mastodon:
  id: "115940357006487323"
  username: "tolhurst"
  hostname: "Techhub.social"
bluesky:
  id: "bafyreiet64fazuk46twxliit6gmkztmw3cwnavya6tspqwbxh23mpllr2q"
  url: "at://did:plc:xs3efpengqy2qyuhpy3lpdhm/app.bsky.feed.post/3mczvmfbhhi2e"
  link: "https://bsky.app/profile/did:plc:xs3efpengqy2qyuhpy3lpdhm/post/3mczvmfbhhi2e"
  handle: "tolhurst.org"
  hostname: "bsky.social"
  did: "did:plc:xs3efpengqy2qyuhpy3lpdhm"
---
Apple has used four different CPU architectures for its Macintosh computers.  The second, used around the turn of the century, was PowerPC.  I have an iMac with a G5.  It's not quite as powerful as the G5 Mac Pro, or indeed even a modern Raspberry Pi, but with 1 GB of RAM it **ought** to be able still to run many useful applications rather than being consigned to the scrapheap.

However, what it can run is dependent on its operating system. So which one to choose?

## MacOS 10.4 Tiger

The original OS supplied with the machine looks nice and runs fast, but there is little software available. There's no iTerm and the Terminal.app is poor even for running terminal apps. There is a 'tiger brew' fork of Homebrew available with some modern programs but they take a long time to compile.

## Macos 10.5 Leopard

Also officially supported by Apple, it runs a little slower but has more features. There is a 'Sorbet Leopard' modded version available that streamlines and backports features amd seems to work well. There's iTerm2 and Terminal.app is better so this could be usable as a remote terminal. There's ChickenVNC for running apps remotely but I could't get it to work with modern VNC servers. There's a PPC fork of Macports available - I haven't tried but it says 10.6 is preferred for Macports. There's a web-browser, Aquafox, but support for modern websites is pretty limited.

## Macos 10.6 Snow Leopard

Never officially released for PPC chips, only for Intel, there is a hacked version based on a preview release from before PPC support was removed. This is the recommended OS for Macports but unfortunately I found it to be very unstable and can't recommend it.

## Adelie Linux

This obscure distro seems to be the most recommended for PPC support. (Debian still builds for PPC in Sid but doesn't publish releases.) To my surprise it does actually work (provided you install 'beta 5' and not the latest 'beta 6') ! And for terminal usage it's pretty good - you get a full modern terminal. However X11 graphics acceleration doesn't work. So any desktop apps are frustrating slow.  There are reports of old drivers that did work, and source code patches that might work, but currently no-one cares about PPC platform enough to actually debug this. Perhaps as a consequence of this, Firefox (the supplied browser) won't even run.  Also the Grub bootloader doesn't install properly and requires manual intervention to boot.

## Conclusion

So for terminal work, MacOS 10.5 and Adelie Linux are both acceptable. Beyond that nothing is really usable.

## To do:

Try to find software that runs on Linux framebuffer, perhaps a VNC client, which may run faster than using the usual X11 desktop.

Try MorphOS.
