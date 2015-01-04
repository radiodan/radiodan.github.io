---
layout: page
title:  "Make your own Raspberry Pi radio"
---

Make your own Raspberry Pi radio
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

Steps
---

### 1. Download the pre-made disk image and uncompress it

[Download the disk image](http://dev.notu.be/2014/12/radiodan/) and save it to your computer.

You can usually uncompress the disk image by double-clicking on it.

### 2. Flash a blank SD card with the image

[Follow the instructions]() on the Raspberry Pi site to flash the downloaded disk image onto your SD card. Where the instructions talk about the `wheezy disk image` substitute that for the disk image you've just downloaded.

<p class="todo">Include instructions on renaming the radio at this point?</p>

### 3. Plug everything together

Insert the SD card into the Pi.

If you're using the wi-fi adapter plug that into the Pi. If not, plug the ethernet cable into the Pi and connect to your router or other internet connection.

If you're using a USB audio card plug that into the Pi and plug your speaker into the audio card, making sure to put it into the hole marked with headphones.

If you're not using a USB audio card, plug your speaker into the sound jack on the Pi directly.

Plug the Pi into the power source and wait.

### 4. Connect to wi-fi

<p class="note">If you’re not using a wi-fi adapter, skip straight to the next step.</p>

If you're using a wi-fi adapter, the radio initially won't be able to connect to your wi-fi network. It'll create it's own wi-fi network called `radiodan-configuration`. Connect to that network with another computer or phone and a window should pop-up that lets you configure the network.

The final step will be to press the big red **RESTART** button to restart your radio.

<p class="todo">Link to troubleshooting guide for potential issues?</p>

### 5. Play some radio

When the radio starts up, make sure you connect to the same network as the radio. You can then load the web-based remote control on your computer or phone at [http://radiodan.local](http://radiodan.local).

Press the power button on the top-right of the web remote control to get started.
