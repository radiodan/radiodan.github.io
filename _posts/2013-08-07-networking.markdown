---
layout: post
title:  "Networking in Radiodan"
date:   2013-08-07 10:23:03
author: libbymiller
---

There are two current areas of practical research in radiodan. The first has to do with one of the biggest 
bugbears of working with networked devices, particularly ones with no screen: getting it on the network and 
talking to it. The second is about installation and interaction: choosing the level of flexibility. This post is 
about the work on networking. I'll write up the rest soon.


## The problem with setup/connecting to wifi

For Raspberry Pis in general, people use them either with a screen and keyboard, getting networking information 
using the screen, or else headlessly, i.e. without a screen. This is where the problem comes. Moving the devices 
between networks means that you need to get them on the network to talk to them and for them to talk to the 
outside world, without being able to see the usual information on a screen.

So for example, BBC Salford has a lovely Darlek robot made using a Raspberry Pi, which can be controlled remotely via a 
series of RESTful commands (move forward, speak etc). It has its home network programmed into it 
(probably using [wpa supplicant](https://wiki.archlinux.org/index.php/WPA_supplicant), a linux networking tool that allows you to plug in and use wifi devices and 
specific which networks with passwords that they should attempt to connect to in a textfile.)

<img src="/assets/darlek.jpg" width="500" alt="Knitted Darlek"/>

Move it off a network it knows about and you have to do one of two things in order to connect it up:

* connect the Pi to a screen via its HDMI port and use a keyboard to enter the network information
* connect it up to your own computer via an ethernet connection and share your network with it and then connect to 
it over ssh to use wpa supplicant or similar to get it on a network

The first of these may not be very convenient, because smallish HDMI screens may not be available. Modern TVs 
usually have HDMI sockets, but not all monitors do, and in any case you don't necessarily want to carry one around 
with you. The second approach is feasible with Mac OS X (though not when the wifi network is 
certificate-protected).

Once you have managed to tell the device how to get on to a network, you then may need to connect to it the next 
time you want to talk to it. For a developer working on a Pi, typically you'll want to try something out and reboot it. 

If you are sharing your network with it, you can do this again, either finding the IP address via the console or 
nmap and sshing to it that way, or by installing Avahi on it and thereby giving it a known name so you can connect 
to it on the same network (e.g. 'radiodan.local'). (Typically anything giving out IP addresses using DHCP will 
tend to give out the same one to the same device, but you can't rely on that).

If you have not installed Avahi on it, or if you are on a different network, you will need to find its IP address 
somehow. Again, you will need to either connect it up to a monitor and keyboard to see its IP ('ifconfig'), or use 
nmap or Mac OS X console if you're on the same network / sharing; or use some sort of display connected to the 
GPIO. Or you could make it say its IP address using espeak, which is easy to do but is often hard to hear and 
remember.

## Reconnecting and developing

In the development of Radiodan we always have half an eye on ease of use for future developers. We want to make it 
easy for others who don't have huge amounts of time or great skills in networking on linux-like systems to get 
started. None of the current solutions is very easy. It's a substantial hurdle to getting things working for 
people.

Developers have two distinct problems:

* telling the device about the network
* talking to the device on the network

The two problems have parallels in the consumer area too. Printers, networked web cameras and other consumer 
devices have this problem: they need to get on the network (perhaps with no easy user input device or feedback 
device) and other devices need to talk to them once they are on there. It's obviously something that many 
Raspberry Pi and Arduino developers have thought about. There are also other newer devices like the Imp that try 
to solve this problem (and we'll talk about those in another post).

## Our solution 

For now and to solve our immediate problem, we've taken a similar approach to [the Arduino 
Yún](http://blog.arduino.cc/2013/05/18/welcome-arduino-yun-the-first-member-of-a-series-of-wifi-products-combining-arduino-with-linux/). 
If the Radiodan doesn't find a wifi network it knows about, it broadcasts its own wifi network with a known name 
and uses Avahi to enable the developer to connect to it at a known identifier via ssh. The developer can then ssh in and 
add wifi networks using wpa supplicant. In the future we plan to make it more easily configurable over a web 
interface, but for now, this greatly simplifies the issues we've been having connecting to it on various networks.
