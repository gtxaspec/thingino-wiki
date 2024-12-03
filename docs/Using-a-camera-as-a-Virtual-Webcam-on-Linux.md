Using a thingino camera as a virtual webcam on Linux is pretty easy. A gstreamer pipeline can be created where the input comes directly from the camera's RTSP, and gets piped directly to a v4l2loopback device. Consumers of video can then use the same v4l2 device as if it were a webcam.

You need to install gstreamer on Linux, for instance, on Ubuntu:
```
sudo apt install libgstreamer1.0-0 gstreamer1.0-plugins-base gstreamer1.0-plugins-good gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly gstreamer1.0-libav gstreamer1.0-tools gstreamer1.0-alsa gstreamer1.0-pulseaudio v4l-utils
```

You might also need to install the v4l2-loopback module
```
sudo apt install v4l2loopback-dkms
```

First of all, probe the v4l2loopback:
```
sudo modprobe v4l2loopback video_nr=10
```
This will add a new video device on `/dev/video10`.

Now, let's assume the thingino camera is on 192.168.0.5, so run the following to launch a gstreamer pipeline:

```
gst-launch-1.0 rtspsrc location=rtsp://thingino:thingino@192.168.0.5/ch0 latency=0 buffer-mode=auto ! rtph264depay ! h264parse ! decodebin ! videoconvert ! video/x-raw,format=YUY2 ! tee ! v4l2sink device=/dev/video10
```

This needs to keep running in the background to read the RTSP pipeline into the v4l2 device.


---

### Advanced configuration with audio

```
sudo modprobe v4l2loopback video_nr=10
sudo modprobe snd-aloop
```

aac
```
gst-launch-1.0 rtspsrc location=rtsp://thingino:thingino@172.16.0.1/ch0 latency=0 buffer-mode=none name=src \
    src. ! rtph264depay ! h264parse ! avdec_h264 ! videoconvert ! video/x-raw,format=YUY2 ! queue ! v4l2sink device=/dev/video10 sync=true async=false \
    src. ! rtpmp4gdepay ! aacparse ! avdec_aac ! audioconvert ! audioresample ! queue ! alsasink device=hw:2,0 sync=true async=false

```
opus
```
gst-launch-1.0 rtspsrc location=rtsp://thingino:thingino@172.16.0.1/ch0 latency=0 buffer-mode=none name=src \
    src. ! rtph264depay ! h264parse ! avdec_h264 ! videoconvert ! video/x-raw,format=YUY2 ! queue ! v4l2sink device=/dev/video10 sync=true async=false \
    src. ! rtpopusdepay ! opusdec ! audioconvert ! audioresample ! queue ! alsasink device=hw:2,0 sync=true async=false
```

