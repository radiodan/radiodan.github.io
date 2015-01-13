---
layout: page
title:  "Make your own radio on a Mac OS X laptop or desktop"
---

Make your own radio on a Mac OS X laptop or desktop
===

This guide explains how to use our software on a laptop or desktop machine.

These are the instructions for Mac OS X (tested on 10.9+).

It's intended for developers to use to get started, so we're going to 
install a minimal radio application.

What you need
---

For your radio you'll need the following:

- a laptop or desktop:
    - with a built in speakers, or headphones or a speaker attached
    - Mac OS X (the software will work with other operating systems)
    - [homebrew](http://brew.sh) installed
- an internet connection

Steps
---

### 1. Install MPD

    brew update
    brew install mpd

### 2. Install rabbitmq

    brew install rabbitmq
    rabbitmq-server

### 3. Install node.js

    brew install node.js
    npm install -g npm@latest

### 4. Download this example code and install its dependencies

    git clone https://github.com/radiodan/radiodan-skeleton.git
    cd radiodan-skeleton
    npm install

### 5. Run the server

    npm start

### 6. Go to [http://localhost:5000](http://localhost:5000) in a browser

Control the sound from the web page.

<img src="/assets/skeleton_app_screenshot.png" alt="Screenshot of the skeleton app in a browser"/>


### Troubleshooting

### 1. brew error

    error: The following untracked working tree files would be overwritten by merge:

fix:

    cd /usr/local
    git fetch origin
    git reset --hard origin/master


### 2. No sound

Ensure the sound's turned up on your laptop / machine (obvious, but mine wasn't).

