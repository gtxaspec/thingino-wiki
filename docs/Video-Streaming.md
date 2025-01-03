### Video Streaming Endpoints

The default streamer in Thingino is [prudynt-t](https://github.com/gtxaspec/prudynt-t).
Prudynt offers multiple video streaming endpoints that allow you to access your camera feeds:

**Default RTSP Endpoints:**
- **1080p Feed:** `rtsp://thingino:thingino@ip/ch0`
- **360p Feed:** `rtsp://thingino:thingino@ip/ch1`

You can adjust streaming settings using web interface (Settings -> Streamer).

**ONVIF Support:**

Thingino also supports ONVIF for integrating with network video recorders (NVRs) and other ONVIF-compatible software.

**Default ONVIF Settings:**
- **Username:** `thingino`
- **Password:** `thingino`
- **Host:** `ip`
- **Port:** `80`

To modify the ONVIF settings, you can edit the configuration file located at `/etc/onvif.conf`.

**M-JPEG Stream:**

An M-JPEG is available at

`http://ip/x/mjpeg.cgi`

**Still Image Snapshot:**

You can capture a still image snapshot from your camera using the following URL:

`http://ip/x/image.cgi`

For both M-JPEG and the still image, replace `ip` with the actual IP address of your camera.
The username/password is `root` and your root password (default `root`).
HTTP Basic Authentication is used.
