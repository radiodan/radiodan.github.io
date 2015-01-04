---
layout: page
title:  "Raspberry Pi software"
---

Raspberry Pi software
===

This page explains the default layout of the Raspberry Pi radio.

It's the layout you get if you [install the disk image](/help/tutorials/build-radio.html).

Accessing the device
---

By default, the device has the hostname `radiodan` and broadcasts over mDNS at `radiodan.local`

You can SSH into the device at `pi@radiodan.local` using the password `raspberry`.

Where are things installed?
---

Almost everything is installed in `/opt/radiodan`.

`/opt/radiodan/apps` contains a directory for each installed radiodan application.

What services are included?
---

Services are apps that are designed to run all the time. You shouldn't need to start or stop these services and their behaviour can be changed by modifying their config files.

| Name     | Purpose |
 ------    | ---------
| server   | The radiodan media controller server |
| buttons  | The radiodan physical UI controller  |
| updater  | The software updater application  |
| cease    | An application that listens for a special messager from apps to shut down the system |

Prototype apps
---

These are apps that enable specific radio-like behaviour. The `example` app is a very basic radio with a web-based remote control. The `magic` app is a more fully-featured internet radio that contains a physical user interface, a web based remote control and more complex behaviours such as avoiding programmes.

| Name     | Purpose |
 --------- | ---------
| magic    | The default IP radio application  |
| example  | An example application (not active by default) |

Starting and stopping services
---

`monit` is used to start, stop and restart services. You can list all monitored services using the `sudo monit summary` command. Restart a service using `sudo monit restart <name>` where `<name>` is the name of the service. You can stop services using `sudo monit stop <name>`. To permanently stop a service from running, you should remove it's entry from the monit config file. See the next section for info.

Device types
---

A `device type` is the combination of services and apps that are running at one time. For example, your radio might behave like a **Magic Button** radio where the `server`, `buttons`, `updater` and `cease` services would run as well as the `magic` prototype app.

To change the device type, run the `radiodan-device-type` command. This will list the available types. Switch type by specifying the name.

Switching device types simply changes which `monit` configuration file is currently active. All available config files are in `/etc/monit/monitrc.d/` and active config files are symlinked into `/etc/monit/monitrc.d/`.

To stop a service starting, open the monit config for the current device type and comment-out the lines relating to the serice you want to stop. Some services, such as the updater and cease daemon are in the radiodan-general config file.

<p class="todo">Example of listing device types and switching to a device type.</p>

