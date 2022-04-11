---
layout: page
title: FAQ
subtitle: Frequently Asked Questions
permalink: /software-docs/faq
---

### Where is the dashboard?

`http://<hostname-or-ip>:3000`, where `hostname-or-ip` is the hostname or IP address of your host device. This can be [set during installation](/software-docs/installation#flashing-os-image-using-raspberry-pi-imager), and the IP assignment can be found in most router dashboards.

### My schedules are in the wrong timezone

You should set your host timezone during installation. You can SSH into your host and edit/create the file `/etc/timezone`, where you may specify the timezone. After this you should [run a container update](/software-docs/upgrading).

### My schedules aren't running at the right time

Is it possible they're [in the wrong timezone](#my-schedules-are-in-the-wrong-timezone)?

### The app isn't running

Check out the [Troubleshooting](/software-docs/installation#troubleshooting) section of the installation docs.

### What is the minimum disk space requirement?

You should use an SD card with at least **16 GB** of space. The applications run in docker containers and thus the host will need to pull docker images. These images are between 1 and 2GB in size.

### How do I free up disk space from docker images?

Currently there is no automated way to prune images. You can SSH into your host device and run the following to prune images:
```
docker image prune
```

### Can I use multiple reservoirs with this software?

Yes and no. A single device (such as a raspberry pi) running this software can control **one single reservoir**. However, you can run multiple devices with multiple reservoirs. To avoid hostname collision, be sure to specify different hostnames per device when [flashing the OS image](/software-docs/installation#flashing-os-image-using-raspberry-pi-imager).

### How do I restart the application(s)?

There are a few ways to "reboot" the app:
1. Reboot the host machine - SSH into host device and run `sudo reboot`
2. Restart containers - SSH into host device and run `docker restart autofeed-client` or `docker restart autofeed-server`
3. Power cycle device - if your device is running in a control box for instance, you can flip the power switch off then back on.

### How do I update the application(s)?

Check out the [Uppdating](/software-docs/upgrading) documentation.
