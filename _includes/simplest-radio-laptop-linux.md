Linux: What you'll need
---

For your radio you’ll need the following:

* a laptop or desktop:
     * with a built in speakers, or headphones or a speaker attached
     * Debian-based system such as Ubuntu
* an internet connection


Linux: Steps
---

### 1. Install git

    sudo apt-get install git

### 2. Install MPD

    sudo apt-get update
    sudo apt-get install mpd

### 3. Install and start rabbitmq

    sudo apt-get install rabbitmq
    rabbitmq-server

### 4. Install node.js

    sudo apt-get install node.js
    npm install -g npm@latest

{% capture skeleton %}{% include skeleton.md %}{% endcapture %}
  {{ skeleton | markdownify }}

<!--### Linix: Troubleshooting!>


