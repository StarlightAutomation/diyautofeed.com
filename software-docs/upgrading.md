---
layout: page
title: Upgrading
permalink: /software-docs/upgrading
---

### SSH into Host

SSH into your host device. If you have not setup SSH, you will need to re-flash and follow the Installation Instructions again.

### Run Update Script

The update script is located at `/etc/autofeed/update.sh` and takes two positional arguments:
* App - `server` or `client`
* Image - the docker image to update the app to

#### Updating the Server

Generally you will use versions from the image `ghcr.io/starlightautomation/autofeed-server`. You can technically update the app to any image, but this is not recommended. You should avoid using the `latest` tag as it could cause unintended updates in the future.

```
/etc/autofeed/update.sh server ghcr.io/starlightautomation/autofeed-server:1.2.3
```
You can replace `1.2.3` with any version number you'd like.

#### Updating the Client

Generally you will use versions from the image `ghcr.io/starlightautomation/autofeed-client`. You can technically update the app to any image, but this is not recommended. You should avoid using the `latest` tag as it could cause unintended updates in the future.

```
/etc/autofeed/update.sh client ghcr.io/starlightautomation/autofeed-client:1.2.3
```
You can replace `1.2.3` with any version number you'd like.

#### Syncing App Versions

Image versions are released simultaneously for both apps. There may not always be changes to the app, for instance if there were updates to the `server` but not to the `client`. Generally you should update both apps to the same version with each update.

```
/etc/autofeed/update.sh server ghcr.io/starlightautomation/autofeed-server:1.2.3
/etc/autofeed/update.sh client ghcr.io/starlightautomation/autofeed-client:1.2.3
```
