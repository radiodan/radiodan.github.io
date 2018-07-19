---
layout: page
title:  "Help - Quick Start"
subnav:
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

A [user guide is available](https://docs.google.com/document/d/1EK3uVpX3aAUypNCLpxTcyp-1OTKuV67lFyXnuxzXXLA/edit), which includes running the 
software on a laptop and setting up a Raspberry Pi. The software currently only runs on a Raspberry Pi 3.

<h2 id="audio">Audio</h2>

Linux audio configuration can be very challenging. [This guide](https://radio-docs.netlify.com/docs-audio) contains instructions for configuring 
a variety of audio hardware. We recommend a USB speaker (or [USB soundcard](https://shop.pimoroni.com/products/usb-soundcard)) as the simplest, a 
[pHAT Beat](https://shop.pimoroni.com/products/phat-beat) if you want to use a bare un-amplified speaker, or a [pHAT 
DAC](https://shop.pimoroni.com/products/phat-dac) if you'd rather use a speaker with a 3.5mm jack.

Radiodan software *will not work with the Raspberry PI's default 3.5mm jack output*.

<h2 id="wifi">Wifi</h2>

[This](https://github.com/radiodan/wifi-connect-ui) isn't currently integrated but can be very useful for devces that get moved around - if installed, it creates an access point that you can 
connect to and set your preferred wifi network and channel.

<h2 id="arch">Architecture</h2>

Andrew [has blogged](http://andrewnicolaou.co.uk/posts/2018/browser-as-engine) about this type of architecture, describing Radiodan as an example.

<h2 id="case">Building a case</h2>

The case was designed by [Victor 
Johanssen](http://www.objectsandinteractions.com/). We have [laser cutting templates](https://github.com/radiodan/hardware/tree/master/case) and [instructions for making them](/help/tutorials/make-a-case.html). Our 
current recommendation is to use the wide version of the case with the 
current [bill of materials](https://github.com/radiodan/hardware/tree/master/bom).

<h2 id="pcb">The Radiodan PCB</h2>

It is difficult to fit many buttons and dials on a Raspberry Pi, so we had a 
PCB designed for us. It enables the use of two illuminated RGB push-button 
dials and a simple button.

#### Open Source files

The PCB files are available 
[online](https://github.com/radiodan/hardware/tree/master/pcb) and we've 
successfullly had them made by [Dirty PCB](http://dirtypcbs.com) and [OSHPark](https://oshpark.com). The component part 
numbers are in the PDF of the PCB documentation and there's also a [bill 
of materials](https://github.com/radiodan/hardware/tree/master/bom) with sources.

#### Soldering the PCB

This can be a little confusing, so here are [step by step instructions](https://github.com/radiodan-archive/project/blob/master/docs/physical_ui_pcb_v1.md).

