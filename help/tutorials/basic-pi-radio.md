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

- a Raspberry Pi, we recommend a model B+, but a B is fine too. You can buy them from [Farnell](http://export.farnell.com/rp/order/) or [RS](http://uk.rs-online.com/web/generalDisplay.html?id=raspberrypi) and other places. You need two USB ports if you are either charging your speaker off USB or using a sound card
- a power cable for the Pi
- a micro SD card (minimum 8GB) that you can overwrite. One [suitable for the Pi](http://cpc.farnell.com/samsung/mmctr08gubch-rmlmk-farn-kit/memory-microsd-noobs-java-8gb/dp/SC13458) is best, or try get a reputable make.
- a speaker with a 3.5mm audio jack. We use [a speaker like this one](http://uk.farnell.com/visaton/2901/speaker-miniature-k50-8ohm/dp/4662064) soldered to a 3.5mm jack, but [this play-while charging USB / 3.5mm stand alone speaker](http://www.amazon.co.uk/Veho-Rechargeable-Speaker-iPods-Players/dp/B002CS2T4I/ref=sr_1_1) works too
- (optional) a USB audio adapter [example](http://thepihut.com/products/usb-audio-adapter) (for better sound)
- a Wi-Pi USB wi-fi adapter (RT5370 chipset, like [this one](http://cpc.farnell.com/1/1/110228-dongle-wifi-usb-raspberry-pi-wipi-element14.html) are known to work, others may do) OR an ethernet cable to plug into your router

You'll also need:

- a laptop or other computer with USB 
- An [SD card reader](https://www.google.co.uk/search?q=SD+card+reader) - computers sometimes have them built in, or they can be bought very cheaply.
- A wifi connection - it can be open or password protected (WPA or WEP), but our wifi configuration tool which links the Raspberry PI to a wifi network won't work if it's a captive portal where you have to go through a web page to get connected. It also won't work with proxies at the moment.

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

