---
layout: page
title:  "Help - Quick Start"
subnav:
  -
    title: "Raspberry Pi"
    href: "#pi"
  -
    title: "Audio"
    href: "#audio"
  -
    title: "Wifi"
    href: "#wifi"
  -
    title: "Architecture"
    href: "#arch"
  -
    title: "Case"
    href: "#case"
  -
    title: "PCB"
    href: "#pcb"
---

# Quick Start

Radiodan is designed to be run on a Raspberry Pi 3, 2 or zero. It doesn't 
currently run well on a Pi A, B, or B+, although if, like me, you build the 
card on a B+, the result will run fine on a Zero.

You can also [run it on Mac or Linux](/help/tutorials/simplest-radio-laptop.html), minus the buttons, dials, lights etc.

Some examples of what you can do with it are on the [showcases](/showcases) page.

More detailed instructions are in the [tutorials](/help/tutorials/) pages.

<h2 id="pi">Raspberry Pi</h2>

You will need:

1. Raspberry Pi 2, 3 or Zero
2. 8G or more micro SD card. 4G isn't big enough.
3. 3.5mm-jack speaker
4. If on a Zero: a [DAC](https://shop.pimoroni.com/products/phat-dac) or [HDMI to VGA adaptor](https://thepihut.com/products/raspberry-pi-hdmi-to-vga-convertor?variant=758603141) (to keep the USB port free for the wifi)
5. If on a Pi 2 or Zero: a [supported wifi USB dongle](https://github.com/resin-io/resin-wifi-connect)
6. If on a Zero: a [USB micro to USB A adaptor](https://thepihut.com/products/usb-to-microusb-otg-converter-shim)
7. Power supply for the Pi
8. Laptop and ethernet cable; SD card reader

Download the latest [Raspian Jessie](https://www.raspberrypi.org/downloads/raspbian/).

On a Mac laptop, SD card inserted into a reader, 

    diskutil list
    diskutil unmountDisk /dev/diskn
    sudo dd bs=1m if=~/Downloads/2016-03-18-raspbian-jessie.img of=/dev/rdiskn

("n" was "2" for me. If you are unsure about this, use the [official 
guide to installing operating system images](https://www.raspberrypi.org/documentation/installation/installing-images/) for the Pi).

(Asssuming you're using a Pi 2 or 3), put the SD card in the Pi, plug the 
speaker into the Pi's 3.5mm jack and power it up. If you're on a Zero, do 
the same, but you'll need to follow the <a href="#sound">instructions for 
the DAC or HDMI audio below</a> before you hear anything.

Log in, expand the filesystem (via ```sudo raspi-config```), reboot, log in again, then install Radiodan:

    git clone https://github.com/radiodan/provision
    cd provision
    git fetch origin
    git checkout -b minimal origin/minimal

**Warning: ```provision all``` deletes a lot of programmes that Radiodan doesn't need, e.g the Desktop, Scratch etc. Don't use this command if you are using the Raspberry Pi installation for something else.**

    sudo ./provision all

This part takes about 10 minutes on a 3, 30 minutes on a 2, and a bit longer on a Zero.

You should hear a cheer when it installs successfully. 

After that, then reboot. 

You'll hear a cheer again as it starts up. On your laptop or phone you 
should see a new wifi network called ```"radiodan-configuration"```. Connect 
to that, tell it the wifi details you want it to connect to using the browser popup 
window (if no window appears, go to [http://radiodan.local:8080](http://radiodan.local:8080)).

Reconnect your phone or laptop to that same wifi, and you will be able to 
go to [http://radiodan.local](http://radiodan.local) in a browser and play 
some audio files that way.

### Troubleshooting

#### No access point appears 

Check that your wifi has the right chipset - RT5370. The official Raspberry Pi wifi USB dongles **don't**.
More information about supported dongles is on the [Resin wifi page](https://github.com/resin-io/resin-wifi-connect)

#### [http://radiodan.local](http://radiodan.local) doesn't work

Some networks don't allow UDP packets - in this case you will not be able to 
control Radiodan via another device. We have had some trouble with certain 
corporate networks, networks that work via the power supply and some local 
Android hotspots.

Alternatively if you are on an Android phone, ```.local``` urls are not supported, 
but if you can find the IP addresss of the pi, then you can still control 
it.

<h2 id="audio">Audio</h2>

By default Radiodan will use the 3.5mm jack output, but the Pi's built in 
audio is quite poor. We have had the most success with a [Phat 
DAC](https://shop.pimoroni.com/products/phat-dac) - a board that requires 
soldering but fits onto the GPIO of your Pi. It's designed for the Zero but 
works with the Pi 2 and 3 too.

You can also use a USB sound card (which might be useful if you want to have 
a microphone), or HDMI via some HDMI to VGI converters (might be useful for 
a Zero).

You can ssh to your Radiodan from a machine on the same network using ```ssh pi@radiodan.local```, password ```raspberry```.

### Using DAC audio

Use the [Phat DAC guide](http://learn.pimoroni.com/tutorial/phat/raspberry-pi-phat-dac-install) for setup.

### Using USB audio

[This USB audio adaptor](https://thepihut.com/collections/cables-leads/products/usb-audio-adapter) works well.

    sudo rm /etc/modprobe.d/alsa-base.conf 

reboot, then 

    aplay -l

should say something like

    card 1: Device [USB Audio Device], device 0: USB Audio [USB Audio]

edit ```/usr/share/alsa/alsa.conf``` - look for the part saying ```defaults.ctl.card``` and edit it to match that line from ```aplay - l```. In my case:

    defaults.ctl.card 1
    defaults.pcm.card 1
    defaults.pcm.device 0

### Using HDMI audio via a VGA adaptor

Uncomment these two lines in ```/boot/config.txt```

    # uncomment to force a specific HDMI mode (this will force VGA)
    hdmi_group=1
    hdmi_mode=1

and reboot. 

<h2 id="wifi">Wifi</h2>

If you want to use the wifi part of Radiodan only - for example if you want 
to create another kind of device that needs a user-friendly way of getting 
on the wifi network - you can follow the instructions 
[here](https://planb.nicecupoftea.org/2016/03/20/wifi-connect-quick-wifi-access-point-to-tell-a-raspberry-pi-about-a-wifi-network/).

<h2 id="dev">Developing</h2>

The [skeleton app](https://github.com/radiodan/radiodan-skeleton), written 
by Andrew Nicolaou, shows the basic workings of radiodan, and illustrates 
both serverside and clientside usage. You can see some extensions to this in 
[this Radio 3 'red button' radio 
example](https://github.com/radiodan-demos/r3_red_button). Radiodan ships 
with the skeleton app which you can go in and edit.

You can ssh to your Radiodan from a machine on the same network using ```ssh pi@radiodan.local```, password ```raspberry```.

The main things to know are:

* The [skeleton app](https://github.com/radiodan/radiodan-skeleton) is installed in ```/opt/radiodan/apps/skeleton``` (it may help to do ```chown -R pi:pi``` in that directory)
* Everything is controlled by supervisor, so you can see what's running using ```sudo supervisorctl status``` and restart a component using ```sudo supervisorctl restart [name]```
* Logs are in ```/var/log/radiodan/*``` which is controlled by the files in ```/etc/supervisor/conf.d/``` directory
* More on [architecture](help/architecture.html) 
* [Full documentation](http://radiodan-client.readthedocs.org)
* Buttons and dials are separate - see below - and you may also want to check out the <a href="#pcb">Radiodan PCB</a>.

<h2 id="buttons">Buttons and dials</h2>

To use the buttons and dials, you need to first attach sme buttons and 
dials. Because of the limited number of GPIO pins, the easiest way of doing 
this is with the <a href="#pcb">Radiodan PCB</a>.

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

<h2 id="arch">Architecture</h2>

[Radiodan architecture documentation is available](/help/architecture.html).

<h2 id="case">Building a case</h2>

The case was designed by [Victor Johanssen](http://www.objectsandinteractions.com/). We have [laser cutting 
templates](https://github.com/radiodan/hardware/tree/master/case) and 
[instructions for making them](/help/tutorials/make-a-case.html).

<h2 id="pcb">The Radiodan PCB</h2>

It is difficult to fit many buttons and dials on a Raspberry Pi, so we had a 
PCB designed for us. It enables the use of two illuminated RGB push-button 
dials and a simple button.

#### Open Source files

The PCB files are available 
[online](https://github.com/radiodan/hardware/tree/master/pcb). The
components part numbers are in the PDF of the PCB documentation.

#### Soldering the PCB

This can be a little confusing, so here are [step by step instructions](https://github.com/radiodan-archive/project/blob/master/docs/physical_ui_pcb_v1.md).

