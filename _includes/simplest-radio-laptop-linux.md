Linux: What you'll need
---

For your radio you’ll need the following:

* a laptop or desktop:
     * with a built in speakers, or headphones or a speaker attached
     * Debian-based system such as Ubuntu
* an internet connection


Linux: Steps
---

### Install git

    sudo apt-get install git

### Install MPD

    sudo apt-get update
    sudo apt-get install mpd

### Install golang

    sudo apt-get install -y golang

### Install zeromq

    sudo apt-get install -y --force-yes libzmq3 libzmq3-dev
    sudo apt-get install zeromq

### Install node.js

    sudo apt-get install node.js
    npm install -g npm@latest

{% capture skeleton %}{% include simplest-radio-skeleton.md %}{% endcapture %}
  {{ skeleton | markdownify }}

### Linux: Troubleshooting

