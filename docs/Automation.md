Thingino has features that make it easy to upgrade and configure the camera using only an SD card.

### Upgrade from binary images on SD card

The Thingino bootloader can flash new firmware from an SD card during the boot process.
Copy the new version of the firmware to the root directory of an SD card, rename the firmware file to `autoupdate-full.bin`,
and reboot the camera with the card inserted. The image will be recognized on boot and flashed instead of the existing one.
Upon successful flashing, a stop file named `autoupdate-full.done` will be created on the card to prevent cyclic reflashing.
If you want to reflash another camera using the same card, remove this stop file first.

You can also update the bootloader only. The procedure remains the same, but rename the bootloader image to `autoupdate-uboot.bin` instead.

### Using a file on the SD card to change the U-Boot environment

Provisioning and updating the bootloader environment can be done using the `uEnv.txt` file in the root directory of an SD card.
Create such a file in the following format:

```
parameter1=value
parameter2=multiword value
parameter3='complex value using %{variable} data'
parameter4'
```

Insert the card and reboot the camera. New values will be imported into the bootloader environment, adding to or overwriting existing parameters in it. Values without a definition will be unset (removed) from the bootloader environment.

### Running scripts from an SD card

Thingino recognizes two shell script names on an SD card that are executed on boot:

- `run.sh` will be executed every time the system boots, as long as it is found on the card.
- `runonce.sh` is executed the first time it's found, then a stop file `runonce.done` is created to prevent consecutive executions. Delete this stop file if you need to run the `runonce.sh` script again.