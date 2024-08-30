### Accessing the Web UI

Once you have set up your Thingino device, you can access the web UI to configure and manage your device. The web UI can be accessed through the following URLs:

- **Using the hostname**: `http://hostname.local`
- **Using the IP address**: `http://192.168.1.100` (replace with your actual IP address)

For example, if you set up your device with a hostname of `thingino-device`, you can access the web UI at:

- `http://thingino-device.local`

If you prefer to use the IP address or if hostname resolution is not working, you can access the web UI at:

- `http://192.168.1.100` (replace `192.168.1.100` with the actual IP address assigned to your Thingino device)

![thingino-webui-preview](https://github.com/themactep/thingino-firmware/assets/37488/51378025-8711-4a24-9056-453777fe8315)

### PTZ Controls

In the Thingino Web UI:

- **PTZ (Pan-Tilt-Zoom) Control**: Hover over the preview image to reveal PTZ controls. Adjust the camera's position as needed. To reset the camera to its default position, double-click the circle in the center of the PTZ controls.

### Night Vision Settings

For adjusting night vision:

- **Night Vision Control**: Hover over the bottom of the preview image to bring up the night vision control bar. This bar allows you to adjust night vision settings.

### Infrared Night Vision Configuration

- **Day/Night Trigger Threshold**: Sets the light level at which the camera switches between day and night modes. If the light drops below this level, the camera switches to night mode, potentially using infrared light. When light increases, it switches back to day mode.

- **Day/Night Tolerance**: Acts as a buffer to prevent frequent mode switching due to minor lighting changes. It ensures the camera remains stable even with minor variations in light.

The WebUI also displays the current gain with a sun icon, allowing you to gauge and adjust the camera's light sensitivity for optimal performance.
