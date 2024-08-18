Thingino Web User Interface is available on port 80. 

The default credentials for accessing the Web UI are _root_ for username and _root_ for password (or whatever password you set via the captive portal or via ssh).

![thingino-webui-preview](https://github.com/themactep/thingino-firmware/assets/37488/51378025-8711-4a24-9056-453777fe8315)In the Thingino Web UI, you can easily control PTZ (Pan-Tilt-Zoom) devices by hovering over the preview image. This action reveals the PTZ controls, allowing you to adjust the camera's position. To reset the camera to its default position, simply double-click the circle in the center of the PTZ controls.

For night vision settings, hover over the bottom of the preview image to bring up the night vision control bar. This bar provides quick access to adjust the night vision functionality on your device.

## Infrared Night Vision

The day/night tolerance and thresholds help determine when to switch between day and night modes based on the current lighting conditions. These settings are guided by "gain," which measures the difference between the scene's darkness and the preview image's brightness.

- **Day/Night Trigger Threshold**: This setting defines the light level at which the camera switches modes. If the light drops below this level, it switches to night mode, possibly using infrared light for better visibility. If it's brighter, the camera switches back to day mode.

- **Day/Night Tolerance**: This acts as a buffer to prevent the camera from frequently switching modes due to minor changes in lighting. It requires a more noticeable change in light before the camera switches modes, ensuring stability even when using IR light at night.

Additionally, the WebUI displays the current gain with a sun icon, making it easy to visually gauge and adjust the camera's light sensitivity settings for optimal performance under varying light conditions. This helps to fine-tune the camera's responsiveness to ensure consistent surveillance quality.

## Controls  

- In the Thingino Web UI, you can easily control PTZ (Pan-Tilt-Zoom) devices by hovering over the preview image. This action reveals the PTZ controls, allowing you to adjust the camera's position. To reset the camera to its default position, simply double-click the circle in the center of the PTZ controls.

- For night vision settings, hover over the bottom of the preview image to bring up the night vision control bar. This bar provides quick access to adjust the night vision functionality on your device.