---
layout: page
title:  "Architecture"
---

Architecture
===

The toolkit provides a set of useful features. But to make it do anything, you must create a prototype application. This tells the toolkit what your specific app will do.

<img src="assets/toolkit-prototype-diagram.svg">

Digging deeper, the toolkit is made up of components, a mixture of open source software packages and also custom software written in JavaScript running on [node.js](http://nodejs.org/).

Each component is isolated from all the others and runs independently, communicating by sending messages to the other components via a central event bus.

We've built a client library in JavaScript, which makes it easy to talk to the system from prototype apps, either in a web browser or from a node.js application.

<img src="assets/what-is-radiodan-toolkit-diagram.svg">

<p class="todo">Update diagram to show core radiodan components and another diagram "zooming out" to show device components.</p>


The toolkit works just as well for building media prototypes that run in the cloud, or working on powerful computers. But some parts of the toolkit are specifically aimed at helping embedded linux devices such as the Raspberry Pi to help create a believable radio-like experience.

Core components
---

### Event Bus

We use a [broker](https://github.com/radiodan/broker) written in Go over [ZeroMQ](http://zeromq.org/) for the messaging layer. There are clients for many different languages meaning that you can write prototype apps in many languages.

[Read more about the messaging layer, and the format of messages.](/help/software/messaging.html)

### Media Controller

This  manages media player instances. You send the media controller commands to play audio content. This can be MP3s stored locally or internet audio streams. The media player emits events when there are changes in the system, such as the next track being played or the player being stopped. Multiple players can be created which allows you to play several streams at once (if your audio device supports it).

[Source code](https://github.com/radiodan/radiodan.js)

Device-specific components
---

### Physical UI Controller

Connects to the GPIO pins on a Raspberry Pi and emits events when a button is pressed or a dial turned. Accepts commands to change the colour of RGB LEDs.

[Source code](https://github.com/radiodan/physical-ui)

### Wifi configuration

On start-up, if no wifi network is joined, the Pi will create its own wifi network, the default name is `radiodan-configuration`. Join this wifi network to configure the wifi details for the radio to join. This [code](https://github.com/radiodan/resin-wifi-connect) is forked from the [Resin project](https://github.com/resin-io/resin-wifi-connect).


