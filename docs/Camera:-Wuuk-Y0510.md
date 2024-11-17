The Wuuk Y0510 is an inexpensive camera with a great price point for the quality of the camera.  It's currently seen with two different sensors, either the original, SC4336p or the less common SC401AI.

# Video guide

There is an awesome video from WLTechBlog on the Wuuk which got me started on my Wuuk flashing journey, and it's well worth a watch.  The below written guide is based off the video and details the process used to flash a Wuuk Y0510


[![Awesome video from 
WLTechBlog](https://img.youtube.com/vi/PhXbeY-PBgg/0.jpg)](https://www.youtube.com/watch?v=PhXbeY-PBgg)

# Flashing the device

## Formatting
You **must** use a MBR type formatted sd-card, this will not work with a GPT formatted card.


## Installation script 
Once your sd card is formatted then your should create a directory called `FACTORY` in the root of the sd card, and in the `FACTORY` directory place this [script](https://gist.github.com/wltechblog/bcc30aca647ee8eac5cb80c6b7368b98), naming it`factory_install.sh`.   

At the time of writing the script is as follows, but I'd recommend checking the link above for the upstream source.

```bash
#!/bin/sh
# WUUK Y0510 https://amzn.to/4dFlKv1
#
# Instructions
#
# Note: If we increase uboot beyond 256k this needs to be adjusted.
# Build thingino firmware, up to make pack_full, or grab full firmware file from github releases

# -- UPDATE --
# There are now 2 versions of this camera. Most use the sc4336p sensor, a few have the sc401ai sensor.
# if you install the sc4336p file and don't have video, grab the sc401ai file, rename it to autoupdate-full.bin,
# remove autoupdate-full.done, and reboot the camera to flash the new one.
# ------------

# Copy full thingio image to sd as /autoupdate-full.bin
# Put this script on sd as /FACTORY/factory_install.sh
# Insert SD card and power on camera, wait about 10 minutes, it will reboot a few times along the way.


mount -t vfat /dev/mmcblk0p1 /mnt
if [ ! -f /mnt/autoupdate-full.bin ]
then
	echo "Missing update file, aborting"
	exit
fi
echo "Extracing uboot"
dd if=/mnt/autoupdate-full.bin of=/mnt/u-boot-t31x.bin bs=1k count=256

if [ -f /mnt/u-boot-t31x.bin ] && [ -f /mnt/autoupdate-full.bin ]
then
	rm -f /mnt/autoupdate-full.done
	echo "Flashing uboot"
	flashcp /mnt/u-boot-t31x.bin /dev/mtd0
	echo "Rebooting"
	reboot
else
	echo "Files missing, not flashing"
fi
```

## Firmware

As mentioned above this camera comes with two different sensor varieties.  Don't worry too much about this, the easiest thing to do is pick a firmware, flash it, and get into the web interface of Thingino, if you happen to have picked the wrong one, you won't get any preview video stream and just repeat the process from this point using the alternative firmware.

Links to the two versions to download from the Thingino website, are included here for convenience.

[T31X, SC401AI, SSV6158, 16MB](https://github.com/themactep/thingino-firmware/releases/latest/download/thingino-wuuk_y0510_sc401ai.bin)

[T31X, SC4336p, SSV6158, 16MB](https://github.com/themactep/thingino-firmware/releases/latest/download/thingino-wuuk_y0510_sc4336p.bin)

In the root folder of the sd card place the `.bin` you download, having renamed it `autoupdate-full.bin` 

## Final check & Flashing

Your SD card should be MBR formatted and contain the following
```                                             
├── autoupdate-full.bin
└── FACTORY
    └── factory_install.sh
```

With your camera powered down insert the SD card and power it on.  

The sequence I observed was as follows:

 - Solid red light ~ 15s
 - No light ~ 1m 40s
 - Solid blue light ~ 10s
 - Rapidly flashing blue light ~ 3s
 - Slowly flashing blue light & camera motors moving ~ 15s
 - No lights

When I had an unsuccessful flash (due to using a GPT formatted SD card I would observe slowly flashing blue lights (I had never paired the camera to the Wuuk app or services)

With a successful flashing process, the following files should be present on your SD card, with the creation of two new files, `u-boot-t31x.bin` and `autoupdate-full.done`
```
├── autoupdate-full.bin
├── autoupdate-full.done
├── FACTORY
│   └── firmware_install.sh
└── u-boot-t31x.bin
```

## Accessing the camera

You should now see a wireless access point available with the format:

**THINGINO-xxxx**

Connect to this and you should be able to see the following screen.

![setup](https://github.com/user-attachments/assets/6bf46f9d-6daa-43f2-946f-07c64fc9f808)

Fill in the data and click "Save credentials" then check the details on the following screen are correct and click "Proceed"

![verification](https://github.com/user-attachments/assets/20afb777-0e8f-44e3-abeb-7734b6f36d66)

# Frigate Configuration

[Frigate](https://frigate.video/) is a popular OpenSource, MIT Licensed, NVR solution that can be run at home and the below notes should be considered a starting point on integrating the Wuuk Y0510 into Frigate.

I couldn't reliably get x265 and audio working and this is my testing on an Intel 10th Gen CPU ( i5-10400).  I also have a [Google Coral TPU](https://coral.ai/products/) using a PCI-E interface, although a USB version exists and they are a fairly low cost solution to offload object detection workload from the CPU.

The below assumes you have a working Frigate instance and I'll cover the config in Thingino that works for me currently, I'm hoping as time goes by, this will get refined as we find out more and people will update this wiki.

## Thingino Configuration

In **Settings => Streamer**

### Main Stream
![streamer-main](https://github.com/user-attachments/assets/ca1b29c3-f378-431a-b5da-891e1fe18419)

### Sub Stream
![streamer-sub](https://github.com/user-attachments/assets/d56da9ec-5a95-4bae-a6d5-217e0ee7a60e)

### Audio
![streamer-audio](https://github.com/user-attachments/assets/c0020460-06a2-452e-9b5f-c6ac4ff71db3)

Here's the `prudynt.cfg` if you prefer a text based approach.

```json
version = "1.0";
general : 
{
  loglevel = "INFO";
  imp_polling_timeout = 500;
  osd_pool_size = 1024;
};
rtsp : 
{
  auth_required = true;
  name = "thingino prudynt";
  password = "thingino";
  username = "thingino";
  est_bitrate = 5000;
  out_buffer_size = 500000;
  port = 554;
  send_buffer_size = 307200;
};
sensor : 
{
  model = "sc401ai";
  fps = 25;
  height = 1440;
  width = 2560;
  i2c_address = 0x30;
};
image : 
{
  vflip = true;
  hflip = true;
  ae_compensation = 128;
  anti_flicker = 2;
  backlight_compensation = 0;
  brightness = 128;
  contrast = 128;
  core_wb_mode = 0;
  defog_strength = 128;
  dpc_strength = 128;
  drc_strength = 128;
  highlight_depress = 0;
  hue = 128;
  max_again = 160;
  max_dgain = 80;
  running_mode = 0;
  saturation = 128;
  sharpness = 128;
  sinter_strength = 128;
  temper_strength = 128;
  wb_bgain = 0;
  wb_rgain = 0;
};
stream0 : 
{
  osd : 
  {
    enabled = true;
    font_stroke_enabled = true;
    logo_enabled = true;
    time_enabled = true;
    uptime_enabled = true;
    user_text_enabled = true;
    font_path = "/usr/share/fonts/UbuntuMono-Regular2.ttf";
    logo_path = "/usr/share/images/thingino_logo_1.bgra";
    time_format = "%F %T";
    uptime_format = "Up: %02lud %02lu:%02lu";
    user_text_format = "%hostname";
    font_size = 21;
    font_stroke = 1;
    font_xscale = 100;
    font_yscale = 100;
    font_yoffset = 3;
    logo_height = 30;
    logo_rotation = 0;
    logo_transparency = 255;
    logo_width = 100;
    pos_logo_x = -10;
    pos_logo_y = -10;
    pos_time_x = 10;
    pos_time_y = 10;
    pos_uptime_x = -10;
    pos_uptime_y = 10;
    pos_user_text_x = 0;
    pos_user_text_y = 10;
    start_delay = 1;
    time_rotation = 0;
    time_transparency = 255;
    uptime_rotation = 0;
    uptime_transparency = 255;
    user_text_rotation = 0;
    user_text_transparency = 255;
    font_stroke_color = 0xFF000000;
    font_color = 0xFFFFFFFF;
  };
  audio_enabled = true;
  enabled = true;
  allow_shared = true;
  format = "H264";
  mode = "VBR";
  rtsp_endpoint = "ch0";
  bitrate = 3000;
  buffers = 4;
  fps = 25;
  gop = 20;
  height = 1440;
  max_gop = 60;
  rotation = 0;
  width = 2560;
  profile = 2;
};
stream1 : 
{
  osd : 
  {
    enabled = true;
    font_stroke_enabled = true;
    logo_enabled = true;
    time_enabled = true;
    uptime_enabled = true;
    user_text_enabled = true;
    font_path = "/usr/share/fonts/NotoSansDisplay-Condensed2.ttf";
    logo_path = "/usr/share/images/thingino_logo_1.bgra";
    time_format = "%F %T";
    uptime_format = "Up: %02lud %02lu:%02lu";
    user_text_format = "%hostname";
    font_size = 12;
    font_stroke = 1;
    font_xscale = 100;
    font_yscale = 100;
    font_yoffset = 3;
    logo_height = 30;
    logo_rotation = 0;
    logo_transparency = 255;
    logo_width = 100;
    pos_logo_x = -3;
    pos_logo_y = -3;
    pos_time_x = 3;
    pos_time_y = 3;
    pos_uptime_x = -3;
    pos_uptime_y = 3;
    pos_user_text_x = 0;
    pos_user_text_y = 3;
    start_delay = 1;
    time_rotation = 0;
    time_transparency = 255;
    uptime_rotation = 0;
    uptime_transparency = 255;
    user_text_transparency = 255;
    user_text_rotation = 0;
    font_color = 0xFFFFFFFF;
    font_stroke_color = 0xFF000000;
  };
  audio_enabled = true;
  enabled = true;
  allow_shared = true;
  rtsp_endpoint = "ch1";
  format = "H264";
  mode = "CAPPED_QUALITY";
  bitrate = 1000;
  buffers = 2;
  fps = 25;
  gop = 20;
  height = 360;
  max_gop = 60;
  width = 640;
  profile = 2;
};
stream2 : 
{
  enabled = true;
  jpeg_path = "/tmp/snapshot.jpg";
  jpeg_channel = 0;
  jpeg_quality = 75;
  jpeg_idle_fps = 1;
  fps = 25;
};
websocket : 
{
  enabled = true;
  ws_secured = true;
  http_secured = true;
  name = "wss prudynt";
  usertoken = "";
  loglevel = 4096;
  port = 8089;
  first_image_delay = 100;
};
audio : 
{
  input_enabled = true;
  input_high_pass_filter = false;
  input_agc_enabled = true;
  input_format = "AAC";
  input_bitrate = 32;
  input_sample_rate = 16000;
  input_vol = 80;
  input_gain = 25;
  input_alc_gain = 7;
  input_agc_target_level_dbfs = 10;
  input_agc_compression_gain_db = 0;
  input_noise_suppression = 0;
};
motion : 
{
  enabled = false;
  script_path = "/usr/sbin/motion";
  debounce_time = 0;
  post_time = 0;
  ivs_polling_timeout = 1000;
  cooldown_time = 5;
  init_time = 5;
  min_time = 1;
  sensitivity = 1;
  skip_frame_count = 5;
  frame_width = 16384;
  frame_height = 16384;
  monitor_stream = 1;
  roi_0_x = 0;
  roi_0_y = 0;
  roi_1_x = 16384;
  roi_1_y = 16384;
  roi_count = 1;
};
rois : 
{
  roi_0 = [ 0, 0, 0, 0 ];
};
```

I've found the most reliable way to test things are by restarting the Wuuk after changes, as sometimes I found the stream/codecs didn't always reflect the most recent changes I made.

You can test things on a Linux desktop with mpv installed with:

```bash
mpv --profile=fast rtsp://thingino:thingino@IP-ADDRESS-OF-WUUK:554/ch0 
```
and I also found installing `ffmpeg` and testing with the following command useful:

```bash
ffplay rtsp://thingino:thingino@IP-ADDRESS-OF-WUUK:554/ch0
```
Both mean you can look at the terminal for clues on what issues may be arising and what video/audio codecs are currently being used.

## Frigate Config

```yaml
mqtt:
  host: mosquitto
  topic_prefix: frigate
  client_id: frigate

go2rtc:
  streams:
    wuuk:
      - rtsp://thingino:thingino@IP-ADDRESS-OF-WUUK:554/ch0

cameras:
  wuuk:
    enabled: True
    ffmpeg:
      hwaccel_args: preset-vaapi #Change appropriate to your host hardware
      inputs:
        - path: rtsp://thingino:thingino@IP-ADDRESS-OF-WUUK:554/ch0
          input_args: preset-rtsp-udp
          roles:
            - record
        - path: rtsp://thingino:thingino@IP-ADDRESS-OF-WUUK:554/ch1
          input_args: preset-rtsp-udp
          roles:
            - detect
      output_args:
        record: preset-record-generic-audio-copy
    detect:
      width: 640
      height: 360
      fps: 5
    objects:
      track:
        - person
    record:
      enabled: True
      retain:
        days: 3
        mode: all # change to motion to only record when motion detected.
    onvif:
      host: IP-ADDRESS-OF-WUUK
      port: 80
      user: thingino
      password: thingino

detectors: # Only valid for Google Coral on PCI
  coral:
    type: edgetpu
    device: pci
version: 0.14
```

This is not intended to be a config that is the best possible configuration for Frigate, but is merely documented as a starting point for further refining and development as the community learns more.

So please feel free to update with any good changes you might make!