---
layout: page
title:  "Make your own Raspberry Pi radio"
---

Make your own Raspberry Pi radio
===

This guide explains how to turn a Raspberry Pi into an internet radio using our pre-made disk image.

What you'll need
---

For your radio you'll need the following:

- a Raspberry Pi, we recommend a model B+
- a power cable for the Pi
- an SD (minimum 8GB) that you can overwrite
- a speaker with a 3.5mm audio jack
- a USB audio adapter (for better sound)
- a Wi-Pi USB wi-fi adapter OR an ethernet cable to plug into your router


I have: an [ethernet cable](#ethernet) | [A USB wifi dongle](#wifi) 
===

<a name="ethernet"></a>

{% capture ethernet %}{% include simplest-radio-ethernet-pi.md %}{% endcapture %}
  {{ ethernet | markdownify }}

Next steps
--

You might like to try [programming your own radio](/help/tutorials/index.html#coding).

----

<a name="wifi"></a>

{% capture wifi %}{% include simplest-radio-wifi-pi.md %}{% endcapture %}
  {{ wifi | markdownify }}


Next steps
--

You might like to try [programming your own radio](/help/tutorials/index.html#coding).

