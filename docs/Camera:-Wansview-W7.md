Installation
------------

### No Tool Method

Not only is the W7 a "no-tool" install, but because of the hardware configuration (the WiFi chip is interfaced with the SoC's only USB port), taking this camera apart is pretty much a waste of time anyway.  So grab yourself a known good SD card and prepare to flash.

### Requirements

The trusted source for all information on the Wansview W7 (and much else besides) is Josh at [WLTechBlog](https://github.com/wltechblog/thingino-installers).  You can pick up the v4_boot.bin from his [GitHub repository](https://github.com/wltechblog/thingino-installers) as the initial step for installing Thingino on the W7 (don't forget to download the file in "raw" mode to ensure that the 250kB padded size of the file is maintained).


This first file is loaded onto the SD card as **"v4_boot.bin"**.

The second part of the install is to download the 8MB Thingino firmware package directly from [this current repository](https://github.com/themactep/thingino-firmware).  This is where we run into a very slight problem.  As with many Chinese manufacturer's, it seems that Wansview have at least two distinct versions of the W7 camera fitted in the same case and with no indication of which one you're actually getting.

This isn't a show-stopper, as you can simply try one of the two versions of Thingino firmware and if the first doesn't work, re-flash with the second instead.

The first version is:-   [this Wansview-W7 labelled file](https://github.com/themactep/thingino-firmware/releases/latest/download/thingino-wansview_w7.bin)

The second is:-    [this Galayou-Y4 labelled file](https://github.com/themactep/thingino-firmware/releases/latest/download/thingino-galayou_y4_t23n_atbm6062.bin)

Both are 8MB files.  Whichever fie you use, it needs to be loaded onto the SD card as **"autoupdate-full.bin"**.

I actually purchased my Wansview W7 from Amazon here in Japan, in mid December 2024.  That camera wouldn't load the thingino-wansview_w7.bin file at all (the camera was left in the blue/red LED flash mode for half an hour).  After trying a couple of different SD cards (I suspected that the loader might not like my big, 64GB one) I did eventually see a change ...the camera would reset itself, the white LEDs would switch on for about 20 seconds and then everything would go dead (no red/blue LED, no captive-portal, nothing).  At this point I thought I'd bricked it.

I hadn't taken any notice of the "Galayou" file on the download page, as my camera was labelled and sold as the Wansview W7 (right!?!), but at that point there was pretty much nothing to lose, so I copied the thingino-galayou_y4_t2n_atbm6062.bin over the autoupdate-full.bin file on my SD card, popped it back into the camera and powered-on.  A few seconds later, the blue/red flash sequence started up again, followed by a blue-only flash.  At this point I finally had a Thingino_XXXX captive-portal pop into my list of available access-points and everything from then was plain sailing.

### That "autoupdate-full" file

If something goes wrong with your subsequent set-up, or perhaps you fat-fingered the captive-portal settings, all is not lost.  Pull your SD card back out of the camera and mount it on your PC.  You'll find that you have an extra file, named "autoupdate-full.done".  If you simply delete that file and re-insert the card, you get to make a fresh attempt at the install.  This won't help if you still have the wrong autoupdate-full.bin file, but it does help to short-circuit the SD-card re-write loop when you're trying to troubleshoot (and, of course, if the "autoupdate-full.done" file doesn't exist on your SD card, the camera hasn't attempted to do an update, so the card format may be bad, or perhaps one of the files hasn't been copied over correctly).

