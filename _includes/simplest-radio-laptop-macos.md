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

### Install zeromq

    brew install zeromq

### Install golang

    brew install golang

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

### zeromq library mismatch problem

If you get an error like

    16:03:01 broker.1 |  dyld: Library not loaded: /usr/local/lib/libzmq.4.dylib
    16:03:01 broker.1 |  Referenced from: /Users/libbym/radiodan-skeleton/node_modules/.bin/radiodan…
    16:03:01 broker.1 |  Reason: image not found

First kill the server with Control-c.

Then recompile the broker, like this:

    mkdir work
    export GOPATH=$PWD/work
    export PATH=$PATH:$GOPATH/bin
    mkdir -p $GOPATH/src/github.com/radiodan
    cd $GOPATH/src/github.com/radiodan
    git clone https://github.com/radiodan/broker
    cd broker
    go get github.com/tools/godep
    $GOPATH/bin/godep restore
    go install

    cd radiodan-skeleton
    cp $GOPATH/bin/broker node_modules/.bin/radiodan-broker

Then start the server again

    npm start
