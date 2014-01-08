---
layout: post
title:  "Radiodan v1 Retrospective"
date:   2014-01-08 18:15:00
author:
  name: Andrew Nicolaou
  github: andrewn
---

After finishing up Radiodan v1, and just in time for Christmas, Dan and I got together to have a retrospective on the first part of the project from a technical perspective. We wanted to get an idea of what went well, what could have been better and what we'd do differently. This will help us plan Radiodan v2.

## Good

* Using Ruby, everyone familiar
* Get something up quickly
* No-one worked on the same thing: so we did [cold start](https://github.com/radiodan/cold_start), [buttons](https://github.com/radiodan/frankenpins), [servers](https://github.com/radiodan/bbc_service_api), [products](http://www.flickr.com/photos/nicecupoftea/sets/72157634700900413/) - very impressive
* [Faye](http://faye.jcoglan.com/) is good being used everywhere
* Logging is good and it's easy to add logging

## Bad

* Have to understand [Event Machine](http://rubyeventmachine.com/)
* Missing out on UI-type things available for Javascript (e.g. [loads of easing functions](http://easings.net/) for LED animation)
* Using Javascript difficult because callbacks are difficult to test
* Everything (mostly) runs as a single process
* No-one worked on the same thing: working on the same thing is fun and the outcomes might be better?
* Lack of tests mean lack of confidence about if things works
* Error states and error handling not explicit (e.g. missing file causes uncatchable exception)

## Other

* Perceived performance (updating web UI when you interact with it)
* Actual performance (running loads of Ruby interpreters)
* Need to be careful about how we implement internal messaging so it's obvious

## Recommendations for future versions

- Everything needs to be testable and have running tests
- Everyone needs to follow common development practices
- Keep "spikes/bodges" small and focussed and quickly turn into sustainable code
- Latency/CPU load is going to be a big issue
- More experimentation on the physical side of things -- possibly all working together in focussed groups e.g. created X box prototypes, Y apps
- Clear, readable documentation from the outset
- Everything should be automated
- Loosely coupled, message based
- Keep working in the open
- Make it polished
- Bring in UX expertise to understand users and make it polished

