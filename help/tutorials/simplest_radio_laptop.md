---
layout: page
title:  "Make your own radio on a laptop"
---

Make your own radio on a laptop
===

This guide explains how to use our software on a laptop or desktop machine.

These are the instructions for Mac OS X (I used 10.9.5)

It's intended for developers to use to ge started hacking, so we're goingto 
install a minimal radio application.

What you need
---

For your radio you'll need the following:

- a laptop or desktop with a built in speaker or 35mm audio jack
- an internet connection

Steps
---

### 1. Install MPD

brew update
brew install mpd
mpd

### 2. Install rabbitMQ

brew install rabbitmq
rabbitmq-server

### 3. Install node.js

brew install node.js
npm install -g npm@latest (?)

### 4. Download this example code and install its dependencies

git clone https://github.com/radiodan/radiodan-skeleton.git
cd radiodan-skeleton
npm install

### 5. Run the server

npm start

### 6. Go to http://localhost:5000




### Troubleshooting

### 1. brew error

    error: The following untracked working tree files would be overwritten by merge:

fix:

    cd /usr/local
    git fetch origin
    git reset --hard origin/master


### 2. No sound

Ensure the sound's turned up on your laptop / machine (obvious, but mine wasn't).

