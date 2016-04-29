---
layout: page
title:  "Start hacking on your radio"
---

Start hacking on your radio
===

# Hacking the skeleton app

Radiodan is designed to be changed so that you can make your own radio.

The [skeleton app](https://github.com/radiodan/radiodan-skeleton), written 
by Andrew Nicolaou, shows the basic workings of radiodan, and illustrates 
both serverside and clientside usage. You can see some extensions to this in 
[this Radio 3 'red button' radio 
example](https://github.com/radiodan-demos/r3_red_button). Radiodan ships 
with the skeleton app which you can go in and edit.

The main things to know are:

* The [skeleton app](https://github.com/radiodan/radiodan-skeleton) is installed in ```/opt/radiodan/apps/skeleton``` (it may help to do ```chown -R pi:pi``` in that directory)
* everything's controlled by supervisor, so you can see what's running using ```sudo supervisorctl status``` and restart a component using ```sudo supervisorctl restart [name]```
* logs are in ```/var/log/radiodan/*``` which is controlled by the files in ```/etc/supervisor/conf.d/``` directory
* more on [architecture](help/architecture.html) 
* [full documentation](http://radiodan-client.readthedocs.org)
* Buttons and dials are separate - seee bwlow - and you may also want to check out the Radiodan PCB.

# Buttons and dials

To use the buttons and dials, you need to do this:

Get the latest skeleton with the physical-ui server as a dependency

    sudo chown -R pi:pi /opt/radiodan/apps/*
    cd /opt/radiodan/apps/skeleton
    git pull
    git checkout physical-ui
    npm install --production

Re-export the supervisor config including the new one for physical-ui server

    sudo radiodan-default-app skeleton

You might need to restart the radiodan processes

    sudo supervisorctl restart all

Now, when you press the power button it'll play the cheer mp3. When anything 
plays, the light goes green. It returns to white when nothing is playing.

More documentation [is available](http://radiodan-client.readthedocs.org/en/latest/usage/physical-buttons-and-interface/)





