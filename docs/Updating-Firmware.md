When it comes to installing a newer version of the firmware, there are several ways to do it. Some methods are easier than others, some are more appropriate for different situations. On this page we will try to cover all of them.

First of all, there are two approaches to updating the camera firmware. One is a partial update, where only the kernel, userland applications and the overlay partition are updated, leaving the bootloader and its environment settings intact. We call this *update*. The other is a full update, including the bootloader and the environment, leaving the camera in a pristine state, like after a hard factory reset. We call it *upgrade*.

### From the development environment

In most cases, you will need to update or upgrade your firmware during development. To accommodate this need, we have added two commands to the thingino makefile: `make update_ota` and `make upgrade_ota`. Both need the IP address of the camera as the value of the `IP=` argument. Note that the camera should already be online to use this method.

The usual routine to build and install the new firmware would be as follows:

```
make
make pack
make update_ota IP=192.168.1.10
```

or

```
make
make pack
make upgrade_ota IP=192.168.1.10
```

Although you can skip the `make pack` part, the firmware is automatically packed to meet the `update_ota` requirements.


### From the camera itself

When the camera is installed at its final location, the firmware can be upgraded to a newer version from within the camera Linux. Login to the system via `ssh` and use the `sysupgrade` script to install a newer version of the firmware. Using `sysupgrade` requires a parameter to tell it which version to install:

`sysupgrade -p` - Updates the kernel and rootfs from GitHub releases, leaving the existing bootloader and environment intact.

`sysupgrade -f` - Upgrades bootloader, kernel and rootfs from GitHub releases, wiping the environment and destroying all your customizations.

`sysupgrade /path/to/file.bin` - Installs firmware from a file, usually provided via an SD card, NFS share, or uploaded to the `/tmp/` directory on the camera.
