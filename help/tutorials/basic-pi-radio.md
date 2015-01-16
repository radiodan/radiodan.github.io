---
layout: page
title:  "Make your own Raspberry Pi radio"
---

Make your own Raspberry Pi radio: [Ethernet](#ethernet) | [Wifi](#wifi) 
===

This guide explains how to install turn a Raspberry Pi into an internet radio using our pre-made disk image.

What you need
---

For your radio you'll need the following:

- a Raspberry Pi, we recommend a model B+
- a power cable for the Pi
- an SD (minimum 8GB) that you can overwrite
- a speaker with a 3.5mm audio jack
- a USB audio adapter (for better sound)
- a Wi-Pi USB wi-fi adapter OR an ethernet cable to plug into your router

<a name="ethernet"></a>

{% capture ethernet %}{% include simplest-radio-ethernet-pi.md %}{% endcapture %}
  {{ ethernet | markdownify }}

<a name="wifi"></a>

{% capture wifi %}{% include simplest-radio-wifi-pi.md %}{% endcapture %}
  {{ wifi | markdownify }}

Next steps
--

If you want to change the behaviour of your radio, you can [find out more about how the software is organised on the Pi](/help/software/pi-software.html).
