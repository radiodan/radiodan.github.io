Mac OS X: What you'll need
---

For your radio you’ll need the following:

* a laptop or desktop:
     * with a built in speakers, or headphones or a speaker attached
     * Mac OS X (the software will work with other operating systems)
     * [homebrew](http://brew.sh/) installed
* an internet connection


Mac OS X: Steps
---

### Install MPD

    brew update
    brew install mpd

### Install rabbitmq

    brew install rabbitmq
    rabbitmq-server

### Install node.js

    brew install node.js
    npm install -g npm@latest

{% capture skeleton %}{% include simplest-radio-skeleton.md %}{% endcapture %}
  {{ skeleton | markdownify }}


### Mac OS X: Troubleshooting

### brew error

    error: The following untracked working tree files would be overwritten by merge:

fix:

    cd /usr/local
    git fetch origin
    git reset --hard origin/master


### No sound

Ensure the sound's turned up on your laptop / machine (obvious, but mine wasn't).

