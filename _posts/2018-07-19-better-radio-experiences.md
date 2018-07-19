---
layout: post
title:  "Better Radio Experiences"
date:   2018-07-19 12:16:04 +0100
author:
  name: Libby Miller
  github: libbymiller
---

Since our last post, we've been working on a project called ["Better Radio
Experiences"](https://www.bbc.co.uk/rd/projects/better-radio-experiences) in BBC R&D. As part of that we've [completely
rewritten the Radiodan software](https://github.com/andrewn/neue-radio) so it's much easier to use and mostly runs
in-browser. If you want to build an audio experience running on a Raspberry Pi, you can now:

 * develop it on a laptop
 * transfer it to a Pi by dragging and dropping the files (using Samba)

We've tested it on colleagues at a hackday in which we developed four working Raspberry Pi-based audio prototypes. We were
happy to see that it was quick and easy for new users, with some web development experience, to get started.

If you'd like to try it, start with [Dan's](https://twiter.com/pixelblend) [detailed user guide](https://docs.google.com/document/d/1EK3uVpX3aAUypNCLpxTcyp-1OTKuV67lFyXnuxzXXLA/edit#heading=h.loekujw96bux). A document
describing the [architecture, along with detailed API-level documentation and practical tips on configuring linux audio
devices](https://radio-docs.netlify.com/) is also available.

For those interested in the details of the browser-based approach, [Andrew](https://twitter.com/andrewn) [describes the idea 
in detail on his website](http://andrewnicolaou.co.uk/posts/2018/browser-as-engine).

You can see some examples of what you could build on our [updated showcase](http://radiodan.net/showcase/).
