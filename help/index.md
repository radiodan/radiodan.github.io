---
layout: page
title:  "Help - Quick Start"
---

# Quick start

Radiodan is designed to be run on a Raspberry Pi 3, 2 or zero. It doesn't 
currently install on a Pi B or B+.

You can also [run it on Mac or Linux](/help/tutorials/simplest-radio-laptop.html), minus the buttons, dials, lights etc.

Some examples of what you can do with it are on the [showcases](/showcases) page.

More detailed instructions are in the [tutorials](/help/tutorials/) pages.

## Quick start on a Pi

You will need:

1. Pi 2, 3 or Zero
2. 8G or more micro SD card
3. 3.5mm-jack speaker
4. if on a Zero: a DAC or HDMI to VGA adaptor
5. if on a Pi 2 or Zero: a USB wifi card with a [specific chipset - RT5370 - see this post for more detail](https://planb.nicecupoftea.org/2015/01/23/a-quick-analysis-of-wifi-cards-for-using-a-raspberry-pi-as-an-access-point/)
6. if on a Zero: usb micro to USB A adaptor
7. power supple for the Pi
8. Laptop and ethernet cable; SD card reader

Download the latest [Raspian Jessie](https://www.raspberrypi.org/downloads/raspbian/).

On a laptop, SD card inserted into a reader, 

    diskutil list
    diskutil unmountDisk /dev/diskn
    sudo dd bs=1m if=~/Downloads/2016-03-18-raspbian-jessie.img of=/dev/rdiskn

("n" was "2" for me. If you are unsure about this, use the [official 
guide to installing operating system images](https://www.raspberrypi.org/documentation/installation/installing-images/) for the Pi).

Put the card in the Pi.

Log in, expand the card, reboot, log in again, then:

    git clone https://github.com/radiodan/provision
    cd provision
    git fetch origin
    git checkout -b minimal origin/minimal
    sudo ./provision all

If you have a Pi 3, you need to additionally do the following, to enable the 
wifi to work as an access point:

    sudo apt-get install raspi-config
    sudo BRANCH=next rpi-update

then reboot. On your laptop or phone you should see a new wifi network 
called ```"radiodan-configuration"```. Connect to that, tell it the wifi you 
want it to connect to using the browser popup window, reconnect to that 
wifi, and you will be able to go to 
[http://radiodan.local](http://radiodan.local) in a browser and play some 
audio files that way.

#### Troubleshooting

* No access point: check that your wifi has the right chipset - RT5370
* [http://radiodan.local](http://radiodan.local) doesn't work: some networks 
don't allow UDP packets - in this case this part of Radiodan will not work. 
Alternatively if you are on an Andoird phone, ```.local``` urls are not supported, 
but if you can find the IP addresss of the pi, then you can still control 
it.

### Audio 

By default radiodan will use the 3.5mm jack output, but the Pi's built in 
audio is quite poor. We have head the most success with a [Phat 
DAC](https://shop.pimoroni.com/products/phat-dac) - a board that requires 
soldering but fits onto the GPIO of your Pi. It's designe dofr the Zero but 
works with the Pi 2 and 3 too.

You can also use a USB sound card (which might be useful if you want to have 
a microphone), or HDMI via some HDMI to VGI converters (might be useful for 
a Zero).

#### Using DAC audio

Use the [Phat DAC guide](http://learn.pimoroni.com/tutorial/phat/raspberry-pi-phat-dac-install) forr setup.

#### Using USB audio

@@

#### Using HDMI audio via a VGA adaptor


### Wifi

If you want to use the wifi part only, you can follow the instructions 
[here](https://planb.nicecupoftea.org/2016/03/20/wifi-connect-quick-wifi-access-point-to-tell-a-raspberry-pi-about-a-wifi-network/).

### Developing

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

### Buttons and dials

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

## More detail

### Architecture

[Radiodan architecture documentation is available](/help/architecture.html).

### Building a case

The case was designed by Victor Johanssen. We ahve [laser cutting 
templates](https://github.com/radiodan/hardware/tree/master/case) and 
[instructions for making them](/help/tutorials/make-a-case.html).

### The Radiodan PCB

Itis difficult to fit many buttons and dials on a Raspberry Pi, so we had a 
PCB designed for us. It enables the use of two illuminated RGB push-button 
dials and a simple button.

#### Open Source files

The PCB files are available 
[online](https://github.com/radiodan/hardware/tree/master/pcb). The
components part numbers are in the PDF of the PCB documentation.

#### Soldering the PCB

This can be a little confusing, so here are [step by step instructions](https://github.com/radiodan-archive/project/blob/master/docs/physical_ui_pcb_v1.md).

