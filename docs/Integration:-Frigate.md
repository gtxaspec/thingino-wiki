# Integration Guide: Configuring Thingino Camera with Frigate and go2rtc

This guide explains how to set up the Thingino open-source camera firmware to work with Frigate and go2rtc.

## Prerequisites

1. Thingino Camera Firmware: Ensure the firmware is flashed.
1. Frigate: Installed and operational.
1. go2rtc: Installed as part of the Frigate setup (or as a standalone service).
1. Network access to your Thingino camera. (Replace IP addresses and credentials as necessary.)

## Configuration Steps

1. Set AAC Audio on the Thingino Camera
   1. Access the Thingino camera's web interface or configuration tool.
   1. Set the audio codec to AAC.
      - This is a mandatory requirement for compatibility with go2rtc.
      - Ensure that both the main stream (ch0) and substream (ch1) have AAC audio enabled.
   1. Confirm the RTSP server is enabled and working.
1. Note the RTSP endpoints and Camera IP address of each camera:
   1. Main stream: rtsp://thingino:thingino@[CAMERA_IP]/ch0
   1. Substream: rtsp://thingino:thingino@[CAMERA_IP]/ch1

## Configure go2rtc
Add the RTSP streams to your go2rtc configuration, replacing the `[CAMERA_IP]` with that of your Camera, and `cam1` stream name with any other appropriate name. Example configuration:

```
go2rtc:
  streams:
    cam1:
      - ffmpeg:#input=-timeout 15000000 -i rtsp://thingino:thingino@[CAMERA_IP]/ch0
    cam1_sub:
      - ffmpeg:#input=-timeout 15000000 -i rtsp://thingino:thingino@[CAMERA_IP]/ch1
```

- cam1: Points to the primary RTSP stream (ch0).
- cam1_sub: Points to the substream (ch1).
- Increase the timeout parameter to ensure reliable connectivity for environments with variable network performance.

## Configure Frigate to Use go2rtc Streams
Edit the Frigate configuration file (frigate.yml) to link the go2rtc streams:

```
cameras:
  cam1:
    enabled: true
    ffmpeg:
      output_args:
        record: preset-record-generic-audio-copy
      inputs:
        - path: rtsp://127.0.0.1:8554/cam1?timeout=15
          input_args: preset-rtsp-restream
          roles:
            - record
        - path: rtsp://127.0.0.1:8554/cam1_sub?timeout=15
          input_args: preset-rtsp-restream
          roles:
            - detect
```

- Ensure the preset-record-generic-audio-copy output argument is used to retain AAC audio.
- Define roles for each stream:
   - record: For video and audio recording.
   - detect: For motion detection and analytics.

## Test and Verify Configuration
1. Restart the go2rtc and Frigate services.
1. Open the Frigate Web UI and verify:
   - Both streams are displayed correctly.
   - Audio is functioning.
1. Use logs to check for errors like timeouts or audio codec mismatches.

## Optional: Advanced Features
### Optimize Connectivity

- Increase timeout values if you encounter connectivity issues with the Thingino camera.
- Consider switching to ethernet where available to improve connectivity.

### Optional: Integrate with Scrypted for HKSV

- Use Scrypted to bridge Frigate feeds to HomeKit Secure Video (HKSV).
   1. Note the go2rtc IP address and name of each go2rtc camera and register in Scripted as a RTSP Camera Plugin:
      1. Main RTSP Stream URL: `rtsp://[GO2RTC_IP]:8554/cam1`
      1. Substream RTSP Stream URL: `rtsp://[GO2RTC_IP]:8554/cam1_sub`
- [Dummy MQTT switches](https://www.reddit.com/r/Scrypted/comments/ycmyyv/how_do_i_add_motion_sensor_trigger_via_mqtt/) can be configured in Scrypted to listen to Frigate MQTT motion events.
- Adjust the sensor and fps to match a [HKSV supported frame rate](https://github.com/Supereg/secure-video-specification).
