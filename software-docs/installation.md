---
layout: page
title: Installation
permalink: /software-docs/installation
---

# Pre-Requisites
The software platform is intended to run on a Raspberry Pi or similar device. The device you intend to install the platform on should be `arm64` or `amd64` based, as those are the two architectures supported currently.

### Download OS Image

The latest OS image release can be found on the [Releases Page](https://github.com/StarlightAutomation/autofeed-backend/releases).

![image](https://user-images.githubusercontent.com/44447928/160199892-46112e6b-a6f4-4982-abc1-6cfd899795eb.png)

Select one of the image files according to your CPU architecture/desired Raspbian release. Unzipping this file will result in an `autofeed.img` image.

# Flashing OS Image using Raspberry Pi Imager
First, download and install the [Raspberry Pi Imager](https://www.raspberrypi.com/software/).

Next, select `Use Custom` from the OS image selection screen. Find and set the `autofeed.img` that you downloaded in the last step.

![image](https://user-images.githubusercontent.com/44447928/160200147-3533158c-0211-4e7e-b259-525726f4f065.png)

Now, use the key combination `Ctrl + Shift + X` to open the customization dialog. This screen will allow you to set your hostname, `pi` user password, specify wifi config information, set timezone, etc. All of these are important settings. You should at least set your timezone, as the system relies on this setting for your schedules.

![image](https://user-images.githubusercontent.com/44447928/160200422-f0a8073f-ddf5-4e86-80d3-4f3bae4cd961.png)

Select your storage device and click `Write`. Once complete, insert the SD card into the Raspberry Pi and boot.

## Dashboard
The dashboard can be reached at `http://<hostname>:3000`. If you did not customize your hostname, you will likely be able to reach the device at `http://raspberrypi.local:3000`.

## Troubleshooting
Can't find the dashboard? Try SSH'ing into your device to debug. You will need to have specified the SSH configuration when flashing the OS image.

```
docker ps
```
This command shows running containers on the host device. There should be two containers running:
* `autofeed-server` - the API (which can be located at `<hostname>:8080`)
* `autofeed-client` - the user interface (which can be located at `<hostname>:3000`)

If either of these containers are not running, check the following:
1. Disk Space
2. Attempt a manual run

### Disk Space
Your device should resize the root SD partition to the full card size on first boot. If this didn't happen, you may not have enough disk space to pull docker images. You can check this with `df -h`.

![image](https://user-images.githubusercontent.com/44447928/160200957-353b6d2a-6818-43ac-a610-7d16cf5b94ce.png)

Your `/dev/root` filesystem should be roughly the size of your SD card. If this size is lower (e.g. 4-6 GB), you will need to resize the partition using `raspi-config`. Details on this process can be found [here](https://elinux.org/RPi_Resize_Flash_Partitions).

### Attempt a manual run
First, pull each image:
```
docker pull ghcr.io/starlightautomation/autofeed-server:latest
docker pull ghcr.io/starlightautomation/autofeed-client:latest
```

Next, tag the images according to what the system expects:
```
docker tag ghcr.io/starlightautomation/autofeed-server:latest autofeed-server
docker tag ghcr.io/starlightautomation/autofeed-client:latest autofeed-client
```

Finally, run each container:
```
/etc/autofeed/start-container.sh server
/etc/autofeed/start-container.sh client
```
