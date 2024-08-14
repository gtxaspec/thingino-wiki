### Video Streaming Endpoints

Thingino provides several video streaming endpoints that you can use to access your camera feeds:

**Default RTSP Endpoints:**
- **1080p Feed:** `rtsp://thingino:thingino@ip/ch0`
- **360p Feed:** `rtsp://thingino:thingino@ip/ch1`

You can adjust video settings by editing the configuration file located at `/etc/prudynt.conf`.

**ONVIF Support:**

Thingino also supports ONVIF for integrating with network video recorders (NVRs) and other ONVIF-compatible software.

**Default ONVIF Settings:**
- **Username:** `thingino`
- **Password:** `thingino`
- **Host:** `ip`
- **Port:** `80`

To modify the ONVIF settings, you can edit the configuration file located at `/etc/onvif.conf`.

**Still Image Snapshot:**

You can capture a still image snapshot from your camera using the following URL:

`http://ip/cgi-bin/image.cgi`

Replace `ip` with the actual IP address of your camera.