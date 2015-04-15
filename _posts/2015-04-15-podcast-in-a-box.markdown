---
layout: post
title:  "Podcast In a Box Step by Step"
date:   2015-04-15 11:21:19
author:
  name: Libby Miller
  github: libbymiller
---

<p>Cross-posted from <a href="http://planb.nicecupoftea.org/2015/01/03/raspberry-pi-podcast-in-a-box-step-by-step/">Libby's blog</a></p>

<h1>Introduction</h1>
Podcast-player-in-a-box is a way to associate a physical object (a plastic card) with a possibly-changing list of audio files. When you put the card in the box it plays the audio.

It's inspired by <a href="https://gist.github.com/wkjagt/814b3f62ea03c7b1a765">this lovely project to make an audiobook reader</a> and also by <a href="http://www.bbc.co.uk/blogs/legacy/researchanddevelopment/2012/11/building-an-internet-of-playth.shtml">Jasmine Cox's enchanted objects</a>.

I'm particularly interested in using it with <a href="https://huffduffer.com">Huffduffer</a>, an excellent site that enables you to build your own podcast of audio files.

Podcast-player-in-a-box matches contactless cards of a particular type (<a href="http://en.wikipedia.org/wiki/MIFARE">MIFARE</a>) with podcast feeds. MIFARE cards are very common - <a href="http://en.wikipedia.org/wiki/Oyster_card">Oyster cards</a> for example, and many ID cards, so there are plenty of them around (I had 6 in my house, or you can <a href="http://www.amazon.co.uk/gp/product/B00IORWW20">buy them easily</a>), and there's a <a href="http://uk.farnell.com/nxp-explore-nfc">cheap and easily available shield for them</a> for the Raspberry Pi.

The box enables you to "programme" a card for a particular podcast. It doesn't actually write to the card, just reads the id and maintains matches between card ids and urls. A card has to be present to play, and when the box is shut it stops playing. If it finds a new item in the podcast, it plays that, otherwise it remembers roughly where you last were in the podcast.

<a href="/assets/piab/img_3914.jpg" ><img class="alignnone size-large wp-image-615" src="/assets/piab/img_3914.jpg?w=660" alt="IMG_3914" /></a>

I made it because I want to listen to audio podcasts on a device, rather than a mobile or a laptop, because that's how I listen to the radio. I also want to be able to switch between different podcasts very quickly, easily and intuitively.

It's also a test for me of <a href="http://radiodan.net">Radiodan</a>, the radio prototyping platform we've been working on. Radiodan allows you to add new radio apps and flip between them. I wanted to see how quickly I could prototype something using the platform (answer - <a href="http://planb.nicecupoftea.org/2014/12/05/huffduffer-radiodan/">I got quite far in a day</a>, but it's taken me a couple of weeks to iron out the bugs).

You can see the podcast-in-a-box in action <a href="https://www.flickr.com/photos/nicecupoftea/15381723854/">in this video</a>.

Here are step-by-step instructions. It'll take about 2 hours once you have the SD card written - so maybe 3-4 hours in total (but you can do something else while the SD card is writing. Much of the 2 hours is also waiting for stuff to install).
<h1>Things you'll need</h1>
<h2>Ingredients</h2>
<ul>
	<li>Raspberry Pi (B or B+, because you need 2 USB ports, I used a B+ and these instructions assume that)</li>
	<li>Mini speaker with USB power / charging and 3.5mm jack (<a href="http://www.amazon.co.uk/Veho-Rechargeable-Speaker-iPods-Players/dp/B002CS2T4I/">example</a>)</li>
	<li><a href="http://uk.farnell.com/nxp-explore-nfc">Explore NFC Raspberry Pi shield</a></li>
	<li>8G or 4G (micro) SD card suitable for the Pi (<a href="http://cpc.farnell.com/samsung/mmctr08gubch-rmlmk-farn-kit/memory-microsd-noobs-java-8gb/dp/SC13458">example</a>)</li>
	<li><a href="http://cpc.farnell.com/element14/wipi/dongle-wifi-usb-for-raspberry-pi/dp/SC12761?Ntt=wipi">WiPi</a> or similar wifi card (RT5370 chipset)</li>
	<li>Power supply for the Pi (<a href="http://cpc.farnell.com/powerpax/sw4544/power-supply-micro-usb-5v-1-8a/dp/PW03772">example</a>)</li>
	<li>Microswitch (<a href="http://www.maplin.co.uk/p/low-cost-standard-microswitch-with-roller-gw73q">example</a>) + 2 screws to attach it</li>
	<li>6 M/M jumper wires (<a href="http://cpc.farnell.com/twin-industries/tw-mp-10/kit-jumper-wire-mach-pin-10pcs/dp/PC01778">example</a>), two attached to crocodile clips</li>
	<li>2 M/F jumper wires (<a href="http://cpc.farnell.com/pro-signal/psg-jmp150mf/jumper-cables-m-f-150mm-pk10/dp/SC13050">example</a>)</li>
	<li>1 RGB LED common cathode (<a href="http://proto-pic.co.uk/5mm-rgb-led-common-cathode/">example</a>)</li>
	<li>Small breadboard ideally with a sticky back (<a href="http://cpc.farnell.com/cyntech/breadboard170red/breadboard-mini-red/dp/PC01594">example</a>)</li>
	<li>3 x 1K resistors</li>
	<li>Oyster card or similar MIFARE card</li>
	<li>Small box with a lid (<a href="http://www.cc-craft.co.uk/treasure-chest-1-pc.aspx">example</a>)</li>
	<li>Thin balsa wood (~ 0.3mm width) or thick card</li>
	<li>A bit of thicker balsa wood (I used 1cm square) or something similar, to trigger the lid button</li>
	<li>Glue (for the balsa wood lid trigger)</li>
	<li>Optionally: keyboard, mouse and screen, HDMI cable (for the Pi)</li>
</ul>
<a href="/assets/piab/rdan_ingredients.jpg"><img class="alignnone size-large wp-image-711" src="/assets/piab/rdan_ingredients.jpg?w=660" alt="rdan_ingredients"  /></a>
<h2>Tools</h2>
<ul>
	<li>Electric drill</li>
	<li>Screwdriver</li>
	<li>Soldering iron and solder</li>
	<li>Laptop</li>
	<li>Hacksaw</li>
</ul>
Putting it all together requires basic linux commands and editing, but no programming.
<h1>Method</h1>
<h2>1. Put the operating system on the SD card</h2>
I recommend using an <strong>8GB</strong> SD card tested with the PI - Radiodan does a lot of writes to the disk and not all cards are up to it. The Radiodan image is Ubuntu Wheezy with some <a href="https://github.com/radiodan">extra Open Source code</a> for playing audio streams, and managing wifi. If you like, you can use a 4GB card instead of 8GB - there's a separate image for that in <a href="http://dev.notu.be/2014/12/radiodan/">this directory</a>.

Get the Radiodan 8GB SD card image:

<code>curl -O http://dev.notu.be/2014/12/radiodan/2014-12-23-radiodan.img.gz</code>

Plug the SD card into the laptop using a card reader. List disks:

<code>$ diskutil list</code>

Find the disk number (e.g. "2"). Unmount that disk.

<code>$ diskutil unmountDisk /dev/diskX</code>

Unzip and write the image in 1 step:

<code>$ gzip -dc /path/to/2014-12-23-radiodan.img.gz | sudo dd of=/dev/diskX bs=1m</code>

This part can take a long time (74 minutes last time I tried). You can speed it up by -
<ul>
	<li>using a separate card reader rather than the built-in Mac one (if that's what you have)</li>
	<li>you can try <code>$ gzip -dc /path/to/2014-12-23-radiodan.img.gz | sudo dd of=/dev/rdiskXXX bs=1m</code> ("rdisk" rather than "disk") - but I find this can corrupt the disk.</li>
</ul>
<h2>2. Assemble the basic elements</h2>
Put the SD card in the Pi, and the wifi card in one of the USB ports. Plug in the speaker into another USB port and into the 3.5mm audio socket. Plug the Pi into the power supply and plug it into the mains. It should look like this:

<a href="/assets/piab/img_3912.jpg">
<img class="alignnone size-medium wp-image-616" src="/assets/piab/img_3912.jpg?w=225" alt="IMG_3912" /></a>
<h2>3. Get the wifi working and test</h2>
Wait a minute or two for it to boot up, and you should see a wifi network appear ("radiodan-configuration").

Connect to this new wifi network with your laptop. A web page should pop up, if it doesn't, go to any web page. You should see a page load with a list of all the wifi networks available. Pick your usual one, and enter the details, and reboot the Pi when instructed.

<a href="/assets/piab/rdan_wifi1.png"><img class="alignnone size-medium wp-image-612" src="/assets/piab/rdan_wifi1.png" alt="rdan_wifi1"  /></a><a href="/assets/piab/rdan_wifi2.png"><img class="alignnone size-medium wp-image-613" src="/assets/piab/rdan_wifi2.png" alt="rdan_wifi2"  /></a><a href="/assets/piab/rdan_wifi3.png"><img class="alignnone size-medium wp-image-614" src="/assets/piab/rdan_wifi3.png" alt="rdan_wifi3"  /></a>

<b>Make sure you <i>rejoin your usual wifi network.</i></b>
<h2>4. Test the vanilla Radiodan</h2>
Once the Pi has rebooted, you have the default Radiodan. It currently acts like an internet radio. You can test this by going to <a href="http://radiodan.local">http://radiodan.local</a> in a web page on your laptop.

You should see something like this:

<a href="/assets/piab/rdan_default.png"><img class="alignnone size-medium wp-image-617" src="/assets/piab/rdan_default.png" alt="rdan_default" /></a>

Click on the power button and you should hear some radio playing. It can take a little while for it to be visible (you might get <code>404 Not Found</code> for a bit).

We're going to change its behaviour by installing another app.
<h2>5. Log into the Radiodan</h2>
If you like you can do this using a keyboard and mouse and screen, but I usually just shell in from my laptop, since the Radiodan is on the wifi. This can be a bit slow depending on congestion in your wifi network.

<code>$ ssh pi@radiodan.local</code>

The password is the default pi password: "<code>raspberry</code>" (without quotes)
<h2>6. Overclock and enable SPI interface</h2>
<code>$ sudo raspi-config</code>

Reboot: <code>$ sudo reboot</code>

Overclock to Medium

Enable the SPI interface (sudo raspi-config -&gt; advanced -&gt; enable SPI)
<h2>7. Disable Radiodan updates</h2>
Radiodan uses Monit to manage its processes. You can see what it's doing by typing this:

<code>$ sudo monit status</code>

We want to disable Radiodan updates (updater_status) in case it overwrites the changes we've made; we also want to remove radiodan-cease (a utility to turn off the radio with the power button being held down, because we use the power button differently); and we're going to replace radiodan-magic which is the default app with our own, so we're going to stop Monit monitoring all those:

<code>$ sudo monit stop updater_status</code>
<br />
<code>$ sudo monit stop radiodan-cease</code>
<br />
<code>$ sudo monit stop radiodan-magic</code>

then you'll see things like this:
<code>
$ sudo monit status</code>
<br />
<code>File 'updater_status'</code>
<br />
<code>status Not monitored</code>
<br />
<code>monitoring status Not monitored</code>
<br />
<code>data collected Fri, 02 Jan 2015 15:02:16
</code>
<h2>8. Download the podcast software</h2>
Radiodan keeps its apps in <code>/opt/radiodan/apps</code>, so we'll put it there.
<code>
$ cd /opt/radiodan/apps
</code>
<br />
<code>
$ sudo git clone https://github.com/libbymiller/radiodan-client-podcast.git
</code>
<br />
<code>
$ cd radiodan-client-podcast/
</code>
<br />
<code>
$ sudo chown -R pi:pi .
</code>

There are two pieces - <a href="https://github.com/libbymiller/radiodan-client-podcast/blob/master/accessCardReader.py">a script in python that only talks to the NFC reader</a>, and some node code (mostly in <a href="https://github.com/libbymiller/radiodan-client-podcast/blob/master/main.js">main.js</a>) that controls the audio and runs a small web server.
<h2>9. Install dependencies</h2>
Install the dependences for node

<code>$ npm install</code>
<br />
and for the python <a href="https://github.com/svvitale/nxppy">nxppy</a> code (for interacting with the NFC reader)
<br />
<code>
$ cd
</code>
<br />
<code>
$ sudo apt-get update
</code>
<br />
<code>
$ sudo apt-get -y install build-essential python2.7-dev python-setuptools cmake
</code>
<br />
<code>
$ curl -O https://bootstrap.pypa.io/get-pip.py
</code>
<br />
<code>
$ sudo python get-pip.py
</code>
<br />
<code>
$ sudo pip install requests
</code>

Install nxppy:
<code>
$ git clone https://github.com/svvitale/nxppy.git
</code>
<br />
<code>
$ cd nxppy
</code>
<br />
<code>
$ sudo python setup.py build install
</code>

(nxppy didn't seem happy being installed with pip, I didn't investigate why).
<h2>10. Install the podcast app</h2>
Monit works using init.d scripts, so we need to add those, so that our app runs when the Pi is booted up.
<code>
$ sudo cp /opt/radiodan/apps/radiodan-client-podcast/init.d/radiodan-huffduffer /etc/init.d/
</code>
<br />
<code>
$ sudo cp /opt/radiodan/apps/radiodan-client-podcast/init.d/radiodan-nfc /etc/init.d/
</code>

and add these to Monit

<code>$ sudo cp /opt/radiodan/apps/radiodan-client-podcast/init.d/radiodan-type-huffduffer /etc/monit/monitrc.d/</code>

Change the config file for the physical UI:
<code>$ sudo pico /etc/init.d/radiodan-buttons</code>

change
<br />
<code>DAEMON_OPTS="/opt/radiodan/apps/magic/current/config/physical-ui-config.json"</code>
<br />
to
<code>DAEMON_OPTS="/opt/radiodan/apps/radiodan-client-podcast/config/physical-ui-config.json"</code>

Make a small edit to the buttons interface:
<code>
$ sudo pico /opt/radiodan/apps/buttons/current/lib/bootstrap.js</code>
<br />
<code>
// Reverse the polarity of the neutron flow
</code>
<br />
<code>
// rgbOpts.reverse = true;
</code>
<br />
<code>
^^^ comment out this line, like this
</code>

Switch to the new app type

<code>$ sudo radiodan-device-type radiodan-type-huffduffer</code>

Reboot to make sure it all comes up.

<code>$ sudo reboot</code>
<h2>11. Check everything's running</h2>
ssh in again

<code>$ ssh pi@radiodan.local</code>

<code>$ ps ax | grep node</code>
<pre> 2126 ?        Sl     0:11 /usr/lib/erlang/erts-6.1/bin/beam -W w -K true -A30 -P 1048576 -- -root /usr/lib/erlang -progname erl -- -home /var/lib/rabbitmq -- -pa /usr/lib/rabbitmq/lib/rabbitmq_server-3.3.5/sbin/../ebin -noshell -noinput -s rabbit boot -sname rabbit@radiodan -boot start_sasl -kernel inet_default_connect_options [{nodelay,true}] -sasl errlog_type error -sasl sasl_error_logger false -rabbit error_logger {file,"/var/log/rabbitmq/rabbit@radiodan.log"} -rabbit sasl_error_logger {file,"/var/log/rabbitmq/rabbit@radiodan-sasl.log"} -rabbit enabled_plugins_file "/etc/rabbitmq/enabled_plugins" -rabbit plugins_dir "/usr/lib/rabbitmq/lib/rabbitmq_server-3.3.5/sbin/../plugins" -rabbit plugins_expand_dir "/var/lib/rabbitmq/mnesia/rabbit@radiodan-plugins-expand" -os_mon start_cpu_sup false -os_mon start_disksup false -os_mon start_memsup false -mnesia dir "/var/lib/rabbitmq/mnesia/rabbit@radiodan" -kernel inet_dist_listen_min 25672 -kernel inet_dist_listen_max 25672
 2554 ?        Sl     0:11 node /opt/radiodan/apps/buttons/current/bin/server /opt/radiodan/apps/radiodan-client-podcast/config/physical-ui-config.json
 2564 ?        Sl     0:11 /usr/local/bin/node /opt/radiodan/apps/radiodan-client-podcast/main.js
 2575 ?        Sl     0:07 node /opt/radiodan/apps/server/current/bin/server /opt/radiodan/apps/magic/current/config/radiodan-config.json
 2942 pts/0    S+     0:00 grep --color=auto node
</pre>
<code>$ ps ax | grep python</code>
<pre> 2541 ?        D      0:28 /usr/bin/python /opt/radiodan/apps/radiodan-client-podcast/accessCardReader.py
 2951 pts/0    S+     0:00 grep --color=auto python
</pre>
Check for errors

<code>$ tail /var/log/radiodan-huffduffer.log</code>
<code>$ tail /var/log/radiodan-nfc.log</code>
<h2>13. Test the podcast app</h2>
<code>$ curl -X POST http://localhost:5000/rssFromNFC -d "feedUrl=http://downloads.bbc.co.uk/podcasts/fivelive/kermode/rss.xml"</code>

You should hear the podcast. Stop it like this:

<code>curl -X POST http://localhost:5000/stopFromNFC</code>

Now shut down the PI, as we're going to attach the NFC reader.

<code>sudo halt</code>
<h2>14. Solder some wires on to the NFC shield</h2>
One of the downsides of using a shield is that it uses most of the pins, even on the B+. We need to have some sort of a signal about what's going on (an LED), and also a button for the closing-box-switching-off feature. The shield doesn't actually use all the pins but it sits on all of them, so we need to solder the wires we need for the RGB led and the button onto some of the unused pins on the shield.

Because it's a B+ there are a couple of spare ground pins available, so I just soldered the 4 pins I needed. Here's a <a href="http://www.element14.com/community/thread/32728/l/question-about-explore-nxp-nfc-expansion-board">list of the pins the NFC shield uses</a>, but it's a bit vague, and I found the spare ones through trial and error.

The soldering is a bit tricky - what seems to work best is to make the pins short, tin them:

<a href="/assets/piab/rdan_wire1.jpg"><img class="alignnone size-medium wp-image-628" src="/assets/piab/rdan_wire1.jpg?w=224" alt="rdan_wire1"  /></a>

and also tin the places where you'll be adding the wires:

<a href="/assets/piab/rdan_nfc1.jpg"><img class="alignnone size-medium wp-image-626" src="/assets/piab/rdan_nfc1.jpg" alt="rdan_nfc1" /></a>

(we'll be using <a href="http://wiringpi.com/wiringpi-and-the-raspberry-pi-model-b/">WiringPi</a> wires 3,4,5,6 in this diagram - I've put a "*" next to them):

<code>$ gpio readall</code>
<pre> +-----+-----+---------+------+---+--B Plus--+---+------+---------+-----+-----+
 | BCM | wPi |   Name  | Mode | V | Physical | V | Mode | Name    | wPi | BCM |
 +-----+-----+---------+------+---+----++----+---+------+---------+-----+-----+
 |     |     |    3.3v |      |   |  1 || 2  |   |      | 5v      |     |     |
 |   2 |   8 |   SDA.1 |   IN | 0 |  3 || 4  |   |      | 5V      |     |     |
 |   3 |   9 |   SCL.1 |   IN | 1 |  5 || 6  |   |      | 0v      |     |     |
 |   4 |   7 | GPIO. 7 |   IN | 1 |  7 || 8  | 1 | ALT0 | TxD     | 15  | 14  |
 |     |     |      0v |      |   |  9 || 10 | 1 | ALT0 | RxD     | 16  | 15  |
 |  17 |   0 | GPIO. 0 |   IN | 0 | 11 || 12 | 0 | IN   | GPIO. 1 | 1   | 18  |
 |  27 |   2 | GPIO. 2 |  OUT | 0 | 13 || 14 |   |      | 0v      |     |     |
 |  22 |   3 | GPIO. 3*|   IN | 1 | 15 || 16 | 0 | OUT  | GPIO. 4*| 4   | 23  |
 |     |     |    3.3v |      |   | 17 || 18 | 0 | OUT  | GPIO. 5*| 5   | 24  |
 |  10 |  12 |    MOSI | ALT0 | 0 | 19 || 20 |   |      | 0v      |     |     |
 |   9 |  13 |    MISO | ALT0 | 0 | 21 || 22 | 1 | OUT  | GPIO. 6*| 6   | 25  |
 |  11 |  14 |    SCLK | ALT0 | 0 | 23 || 24 | 1 | ALT0 | CE0     | 10  | 8   |
 |     |     |      0v |      |   | 25 || 26 | 1 | OUT  | CE1     | 11  | 7   |
 |   0 |  30 |   SDA.0 |   IN | 1 | 27 || 28 | 1 | IN   | SCL.0   | 31  | 1   |
 |   5 |  21 | GPIO.21 |   IN | 1 | 29 || 30 |   |      | 0v      |     |     |
 |   6 |  22 | GPIO.22 |   IN | 1 | 31 || 32 | 0 | IN   | GPIO.26 | 26  | 12  |
 |  13 |  23 | GPIO.23 |   IN | 0 | 33 || 34 |   |      | 0v*     |     |     |
 |  19 |  24 | GPIO.24 |   IN | 0 | 35 || 36 | 0 | IN   | GPIO.27 | 27  | 16  |
 |  26 |  25 | GPIO.25 |   IN | 0 | 37 || 38 | 0 | IN   | GPIO.28 | 28  | 20  |
 |     |     |      0v*|      |   | 39 || 40 | 0 | IN   | GPIO.29 | 29  | 21  |
 +-----+-----+---------+------+---+----++----+---+------+---------+-----+-----+
 | BCM | wPi |   Name  | Mode | V | Physical | V | Mode | Name    | wPi | BCM |
 +-----+-----+---------+------+---+--B Plus--+---+------+---------+-----+-----+
</pre>
We're soldering on the top of the NFC shield.

<a href="/assets/piab/rdan_wire_nfc.jpg"><img class="alignnone size-medium wp-image-627" src="/assets/piab/rdan_wire_nfc.jpg?w=224" alt="rdan_wire_nfc"  /></a>
<h2>15. Assemble the LED components</h2>
I happened to have some common cathode RGB leds - common anode ones are also available, but need different configuations. The cathode RGB LED's longest leg goes to ground and then it's

<code>blue green [cathode] red</code>

We connect them to WiringPi pins 6, 5 and 4 respectively, using the mini breadboard and the resistors

<a href="/assets/piab/rdan_led1.jpg"><img class="alignnone size-medium wp-image-657" src="/assets/piab/rdan_led1.jpg?w=224" alt="rdan_led1"  /></a>

and then add the ground:

<a href="/assets/piab/rdan_led2.jpg"><img class="alignnone size-medium wp-image-658" src="/assets/piab/rdan_led2.jpg?w=224" alt="rdan_led2"  /></a>
<h2>16. Add the button</h2>
This uses WiringPi pin 3 and another ground pin, via the breadboard again:

<a href="/assets/piab/rdan_button1.jpg"><img class="alignnone size-medium wp-image-655" src="/assets/piab/rdan_button1.jpg?w=224" alt="rdan_button1"  /></a>

The "COM" terminal of the switch goes to ground and the pin 3 wire goes to "NO" (normally open)

<a href="/assets/piab/rdan_button2.jpg"><img class="alignnone size-medium wp-image-656" src="/assets/piab/rdan_button2.jpg?w=224" alt="rdan_button2"  /></a>
<h2>17. Try it all out - Programme a card</h2>
<ul>
	<li>Turn on the Pi and wait until you the LED goes blue</li>
	<li>Go to <a href="http://radiodan.local/">http://radiodan.local/</a> and click on "<a href="http://radiodan.local/write">programme a card</a>"</li>
</ul>
<a href="/assets/piab/rdan_ui.png"><img class="alignnone size-medium wp-image-690" src="/assets/piab/rdan_ui.png" alt="rdan_ui"  /></a>
<a href="/assets/piab/rdan_write1.png"><img class="alignnone size-medium wp-image-691" src="/assets/piab/rdan_write1.png" alt="rdan_write1"  /></a>
<ul>
	<li>Put your Oyster card on the reader (the aerial is the blank bit) and click "next".</li>
	<li>Add a feed URL, e.g <a href="http://downloads.bbc.co.uk/podcasts/fivelive/kermode/rss.xml">http://downloads.bbc.co.uk/podcasts/fivelive/kermode/rss.xml</a> (that one's from the <a href="http://www.bbc.co.uk/podcasts">BBC's podcast site</a>) or one from the excellent Huffduffer (e.g. <a href="https://huffduffer.com/search/rss?q=Scifi">search for Scifi</a>)</li>
</ul>
<a href="/assets/piab/rdan_write2.png"><img class="alignnone size-medium wp-image-692" src="/assets/piab/rdan_write2.png" alt="rdan_write2"  /></a>
<a href="/assets/piab/rdan_write3.png"><img class="alignnone size-medium wp-image-693" src="/assets/piab/rdan_write3.png" alt="rdan_write3"  /></a>
<ul>
	<li>Save</li>
</ul>
<a href="/assets/piab/rdan_write4.png"><img class="alignnone size-medium wp-image-694" src="/assets/piab/rdan_write4.png" alt="rdan_write4"  /></a>

After a few seconds it should start playing the audio from your feed and the light should go green.
<h2>18. Test behaviour</h2>
<ul>
	<li>Click the switch shut - while you hold it, it should stop the audio and the light should go blue</li>
	<li>Release the switch and it should restart the audio and the light should go green</li>
	<li>Remove the Oyster card and it should stop the audio again, and the light should go green</li>
	<li>Add the Oyster card again and it should restart from approximately the same point</li>
</ul>
The basics are now done - we just need to put it in the box. Turn it off by unplugging it or doing <code>sudo halt</code> if you are sshd in to the Pi.
<h2>19. Drill holes in the box</h2>
The basic part is the hole for the power cable. Make a note of the maximum width and height of the small end of the power cable - that's the hole size you need.

<a href="/assets/piab/rdan_microusb.jpg"><img class="alignnone size-medium wp-image-665" src="/assets/piab/rdan_microusb.jpg?w=225" alt="rdan_microusb"  /></a><a href="/assets/piab/rdan_power.jpg"><img class="alignnone size-medium wp-image-664" src="/assets/piab/rdan_power.jpg?w=224" alt="rdan_power"  /></a>

You may also want to add holes for ventilation - it can get warm (but not very hot).

<a href="/assets/piab/rdan_vent.jpg"><img class="alignnone size-medium wp-image-663" src="/assets/piab/rdan_vent.jpg?w=224" alt="rdan_vent" /></a>

<h2>20. Add the switch</h2>

Screw the switch on to the side of the box. Glue a bit of balsa wood or similar in the opposite corner of the lid, and test that when the box is shut you can hear the switch click.

<a href="/assets/piab/rdan_switch.jpg"><img class="alignnone size-medium wp-image-670" src="/assets/piab/rdan_switch.jpg" alt="rdan_switch" /></a>

While you are sawing, cut a couple of pieces of balsa wood, one to fit exactly across the lid and another across the width of the box to form a shelf.

<a href="/assets/piab/rdan_lid.jpg"><img class="alignnone size-medium wp-image-671" src="/assets/piab/rdan_lid.jpg" alt="rdan_lid"  /></a><a href="/assets/piab/rdan_shelf.jpg"><img class="alignnone size-medium wp-image-672" src="/assets/piab/rdan_shelf.jpg" alt="rdan_shelf" /></a>
<h2>21. Put everything in the box</h2>
Put everything in the box threading the power cable through the hole you drilled earlier. The arrangement will vary a bit depending on your box size and shape, but the important things are that the aerial of the NFC reader is accessible (the card doesn't have to be flat on it though) and the LED is visible. Reconnect the croc clips to the switch.

<a href="/assets/piab/rdan_inbox.jpg"><img class="alignnone size-medium wp-image-674" src="/assets/piab/rdan_inbox.jpg" alt="rdan_inbox" /></a>

I've added a little shelf in to make it easier to place the card. The range of the NFC is about 3-5 cm, but the closer the shelf is to it the better.

<a href="/assets/piab/rdan_box_shelf.jpg"><img class="alignnone size-medium wp-image-675" src="/assets/piab/rdan_box_shelf.jpg" alt="rdan_box_shelf" /></a>
<h2>22. Test again</h2>
<a href="/assets/piab/rdan_box_test.jpg"><img class="alignnone size-medium wp-image-676" src="/assets/piab/rdan_box_test.jpg?w=225" alt="rdan_box_test" /></a>

<a href="/assets/piab/rdan_card_shelf.jpg"><img class="alignnone size-medium wp-image-677" src="/assets/piab/rdan_card_shelf.jpg?w=225" alt="rdan_card_shelf" /></a>
<h2>DONE</h2>
You can programme more cards and stick pictures on them to show what they will play. A <a href="http://www.ebay.co.uk/bhp/polaroid-pogo-printer">Pogo printer</a> is a great for this (but a normal printer and a pritt stick work perfectly well too).

<a href="/assets/piab/rdan_cards2.jpg"><img class="alignnone size-large wp-image-714" src="/assets/piab/rdan_cards2.jpg?w=660" alt="rdan_cards2" /></a>

<a href="/assets/piab/rdan_cards1.jpg"><img class="alignnone size-large wp-image-713" src="/assets/piab/rdan_cards1.jpg?w=660" alt="rdan_cards1" /></a>
