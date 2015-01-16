Raspberry Pi with wifi: Steps
---

{% capture pidiskimage %}{% include pi-disk-image.md %}{% endcapture %}
  {{ pidiskimage | markdownify }}

### 3. Plug everything together

Insert the SD card into the Pi.

Plug the wifi adaptor into one of the Pi's USB ports.

If you're using a USB audio card plug that into the Pi and plug your speaker into the audio card, making sure to put it into the hole marked with headphones.

If you're not using a USB audio card, plug your speaker into the sound jack on the Pi directly.

Plug the Pi into the power source and wait.

### 4. Connect to wi-fi

If you're using a wi-fi adapter, the radio initially won't be able to 
connect to your wi-fi network. It'll create it's own wi-fi network called
`radiodan-configuration`. Connect to that network with another computer
or phone and a window should pop-up that lets you configure the network.

<img src="/assets/radiodan_wifi_step1.png" alt="Radiodan wifi step 1: Show networks"/>
<img src="/assets/radiodan_wifi_step2.png" alt="Radiodan wifi step 2: Enter password"/>

The final step will be to press the big red **RESTART** button to restart 
your radio.

<img src="/assets/radiodan_wifi_step3.png" alt="Radiodan wifi step 3: restart"/>


{% capture playradioweb %}{% include play-radio-web.md %}{% endcapture %}
  {{ playradioweb | markdownify }}

<!-- Raspberry Pi with wifi: troubleshooting -->
