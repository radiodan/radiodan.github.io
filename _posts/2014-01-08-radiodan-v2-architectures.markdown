---
layout: post
title:  "Radiodan v2 Architectures"
author: andrewnicolaou
---

We're starting work on Radiodan v2, hot off the back of our [learnings from v1](retrospective).

Our goal is to make v2 much more decoupled, with all the bits of software sending each other messages, rather than talking to each other directly. We've experimented with this before in [other projects](http://www.bbc.co.uk/rd/blog/2013/07/the-egbox-html5-television-prototype) and found it quite promising. We hope this will make the system:

- more reliable - if one part fails, it doesn't bring down everything;
- testable - each component listens and sends a small number of messages that are well-defined;
- language agnostic - if you want to write an app in Python or some other language, you just need to be able to send the correct messages;
- more flexible - you can include or not include components as you wish e.g. don't include the physical interface if you're not running on an embedded device.

## Radiodan Example

We started off by sketching out the architecture of our current [Radiodan Example app](https://github.com/radiodan/radiodan_example). It's mostly a monolithic Ruby application. All the code is loaded in the same process on the machine. If something throws an error (which it does fairly frequently) then the whole app crashes and restarts.

![Example app for Radiodan v1](/assets/v2-arch-post/01-radiodan-example-original.jpg)

We then sketched out how the app would look if everything was decoupled and communicated via messages:

![Example app for Radiodan v2](/assets/v2-arch-post/02-radiodan-example-v2.jpg)

- Blue post-its are software components.
- Green post-its are protocols.
- The arrows shows where components send messages to each other.

## Messages

We came up with a list of core messages that the system would send and listen to.

![](/assets/v2-arch-post/04-core-events.jpg "Core Radiodan events")

We also thought through the errors that could arise in the core server:

![](/assets/v2-arch-post/04-errors.jpg "Core Radiodan errors")

## Other applications

Next, we looked at a few other apps, some that Libby has already built and some that we want to build in the future.

![Radio Democracy](/assets/v2-arch-post/03-radiodanocracy.jpg "Radio Democracy - vote for your favourite programmes")

![Integration with BBC Playlister](/assets/v2-arch-post/05-playlister.jpg "Integration with BBC Playlister")

In this diagram, yellow post-its denote application-specific messages.

Some ideas that we had in our team for providing extra information within and around programmes:

1. "Tell Me More" gives you extra information about a topic mentioned in a radio documentary.

!["Tell Me More" flow](/assets/v2-arch-post/08-tell-me-more-flow.jpg)
!["Tell Me More"](/assets/v2-arch-post/06-tell-me-more.jpg)

2. "Difficulty Dial" allows you to change the difficulty of a programme if you don't understand parts of it:

!["Difficulty Dial" flow](/assets/v2-arch-post/07-difficulty-dial-flow.jpg)
!["Difficulty Dial"](/assets/v2-arch-post/09-difficulty-dial.jpg)

What if we rebuilt the [Olinda social radio](/assets/v2-arch-post/) add-on today?

![Olinda interface sketch](/assets/v2-arch-post/11-olindan-interface.jpg)

The interface above has a picture and light for each of your friends. When your friend is listening to something on their Radiodan then their light switches on. If you press the button, your Radiodan will start playing what they can hear.

![Olinda social radio](/assets/v2-arch-post/10-olindan-social.jpg)

By considering real-world applications of the new architecture we have been able to identify essential components and considerations of the new system.
