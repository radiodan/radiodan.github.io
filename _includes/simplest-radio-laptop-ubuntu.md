Ubuntu: What you'll need
---

For your radio you’ll need the following:

* a laptop or desktop:
     * with a built in speakers, or headphones or a speaker attached
     * Ubuntu 14 or newer
* an internet connection


Ubuntu: Steps
---

### 1. Install MPD

    sudo apt-get update
    sudo apt-get install mpd

### 2. Install and start rabbitmq

    sudo apt-get install rabbitmq
    rabbitmq-server

### 3. Install node.js

    sudo apt-get install node.js
    npm install -g npm@latest

{% capture skeleton %}{% include skeleton.md %}{% endcapture %}
  {{ skeleton | markdownify }}


### Ubuntu: Troubleshooting


