### How to Choose a Compatible Device for Thingino

> [!IMPORTANT]
> Thingino is a DIY project that may require disassembly and some advanced computer skills. While the developers strive to ensure that all procedures and software are safe, reliable, and as user-friendly as possible, users should be prepared for the technical nature of the project. It’s important to be aware that, in rare cases, unforeseen circumstances could lead to device damage or corruption. As such, users should proceed with caution and be prepared for potential challenges.

When selecting a device to use with Thingino, consider the following factors:

**a. Device Type:**
   - **PTZ (Pan-Tilt-Zoom):** If you need a camera that can pan, tilt, and zoom, consider PTZ models. These are ideal for larger areas where you want more control over the viewing angle.
   - **Indoor Cameras:** Choose this type if you need a camera for monitoring indoor spaces. They are generally smaller and more aesthetically pleasing for home or office use.
   - **Outdoor PTZ Cameras:** These are designed for outdoor use and offer PTZ functionality while being weather-resistant.
   - **Outdoor Weatherproof Cameras:** Ideal for fixed-angle monitoring in outdoor environments. These cameras are built to withstand various weather conditions.
   - **Doorbell Cameras:** If you need a smart doorbell with camera functionality, look for doorbell camera models that are compatible with Thingino.

**b. Confirmed Working Devices:**
   - Visit [Thingino.com](https://thingino.com) for a list of devices that have been thoroughly tested and confirmed to work with Thingino. This list is regularly updated based on community feedback and internal testing.

**c. Choosing Your Own Ingenic-Based Device:**
   - If you choose to use a device that isn’t listed on Thingino.com, ensure it features an Ingenic processor, as Thingino is optimized for Ingenic-based devices commonly found in many affordable IP cameras. Before making a purchase, review the device’s specifications or consult the community to verify compatibility. Be prepared to undertake tasks such as disassembling the device, photographing and documenting the PCB, connecting to UART ports to access boot logs, and dumping the firmware. For detailed instructions, refer to the porting guide.

### Determining How to Install Thingino

Once you have your device, there are several methods to install Thingino depending on your device's capabilities:

**a. Install Using USB (If USB Data Works):**
   - If your device supports USB data transfer, you can install Thingino directly via USB. This is often the simplest method, requiring minimal technical knowledge. At a minimum, this may require disassembly, but not modification of the device.  Follow the detailed [Ingenic USB Cloner](https://github.com/themactep/thingino-firmware/wiki/Ingenic-USB-Cloner) guide available in the wiki.

**b. Install via No-Tool Installation:**
   - Some devices support a [no-tool installation](https://github.com/themactep/thingino-firmware/wiki/No-Tool-Installation) method, allowing you to flash Thingino without any special hardware tools. This method is ideal for users who want a straightforward installation process, with no device disassembly required. Device specific instructions can be found in the wiki.

**c. Install via Chip Flash Programmer:**
   - For advanced users, or if other installation methods are not feasible, you can use a chip flash programmer to install Thingino. This method requires disassembling the device and connecting a programmer to the device's flash chip. It’s recommended for users with experience in hardware programming.

### How to Access Your Camera Running Thingino

After successfully installing Thingino, you can access your camera through various methods after completing [Network Setup](https://github.com/themactep/thingino-firmware/wiki/Configuring-Wi%E2%80%90Fi-Access):

**a. Via RTSP:**
   - Thingino supports RTSP (Real-Time Streaming Protocol), allowing you to stream video from your camera to any RTSP-compatible player or software. The RTSP stream URL can be found in the camera's preview page after installation.

**b. Via Built-in Preview Page:**
   - Thingino includes a built-in web interface that allows you to preview your camera’s video feed directly in a web browser. This is a quick and convenient way to check the camera's output without additional software.

**c. Via ONVIF:**
   - For users integrating their camera into a larger security system, Thingino supports ONVIF (Open Network Video Interface Forum) protocol. This allows your camera to be detected and managed by ONVIF-compatible network video recorders (NVRs) and software.  It is enabled by default.

