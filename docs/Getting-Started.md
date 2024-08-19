### How to Choose a Compatible Device for Thingino

> [!IMPORTANT]
> Thingino is a DIY project that may require disassembly and some advanced computer skills. While the developers strive to ensure that all procedures and software are safe, reliable, and as user-friendly as possible, users should be prepared for the technical nature of the project. It’s important to be aware that, in rare cases, unforeseen circumstances could lead to device damage or corruption. As such, users should proceed with caution and be prepared for potential challenges.

When selecting a device to use with Thingino, consider the following factors:

**a. Device Type:**  
   - Thingino supports a variety of devices, including indoor and outdoor cameras, fixed-angle and PTZ (Pan-Tilt-Zoom) models, and smart doorbell cameras. Whether you need a basic indoor camera, a weatherproof outdoor model, or advanced PTZ functionality, Thingino offers compatibility with a wide range of devices for various use cases.

**b. Confirmed Working Devices:**
   - Visit [Thingino.com](https://thingino.com) for a list of devices that have been thoroughly tested and confirmed to work with Thingino. This list is regularly updated based on community feedback and internal testing.

**c. Choosing Your Own Ingenic-Based Device:**
   - If you choose to use a device that isn’t listed on Thingino.com, ensure it features an Ingenic SoC, as Thingino will work only on cameras that use Ingenic-based SoCs that power many affordable IP cameras. Before making a purchase, review the device’s specifications (if possible) or consult the [[community|Resources-and-Links#information]] to verify compatibility with our [[supported hardware|Tech-Info-‐-Supported-Hardware]]. Be prepared to undertake tasks such as disassembling the device, photographing and documenting the PCB, [[connecting to UART ports|UART-Connection]] to access boot logs, and dumping the firmware. For detailed instructions, refer to the [[porting guide.|Porting-Guide]]

### Backup Your Existing Firmware

> [!WARNING]  
> We **strongly recommend** using Cloner to create a **full backup** of the existing stock firmware.

Decide if you want to revert to stock in the future. This is an essential step if you ever need to restore the original functionality or analyze the stock firmware for compatibility. At a minimum, this may require disassembly, but not modification of the device. Follow the [Ingenic USB Cloner](https://github.com/themactep/thingino-firmware/wiki/Ingenic-USB-Cloner) guide to perform a full backup.

### Determining How to Install Thingino

Once you have your device, there are several methods to install Thingino depending on your device's capabilities:

**a. Install Using USB (If USB Data Works):**
   - If your device supports USB data transfer, you can install Thingino directly via USB. This is often the simplest method, requiring minimal technical knowledge. If you already performed a backup using Cloner, this is the most straight forward method. Follow the detailed [Ingenic USB Cloner](https://github.com/themactep/thingino-firmware/wiki/Ingenic-USB-Cloner) guide available in the wiki. 
   - Note that the usb cords included with cameras typically do not have data lines, you will need to provide your own tested cord. Also note that the presence of a USB port on the camera does not necessarily mean that USB data transfer is possible on the camera; the port may be used just to power the camera.

**b. Install via No-Tool Installation:**
   - Some devices support a [no-tool installation](https://github.com/themactep/thingino-firmware/wiki/No-Tool-Installation) method, allowing you to flash Thingino without any special hardware tools. This method is ideal for users who want a straightforward installation process, with no device disassembly required. Device specific instructions can be found in the wiki.

**c. Install via Flash Chip Programmer:**
   - For advanced users, or if other installation methods are not feasible, you can use a [flash chip programmer](https://github.com/themactep/wiki/blob/master/hacking/ch341a-programmer.md) to install Thingino. This method requires disassembling the device and connecting a programmer to the device's flash chip. It’s recommended for users with experience in hardware programming.

**d. Install via U-Boot/SD-Card:**
   - Some cameras can be flashed via SD Card from the stock UBoot bootloader prompt.  This method requires that you access and then
    interrupt the stock firmware's boot process via the [[UART console|UART-Connection]], load the image from the SD Card, and
    flash it via UBoot's flash write commands.

### How to Access Your Camera Running Thingino

After successfully installing Thingino, you can access your camera through various [media endpoints](https://github.com/themactep/thingino-firmware/wiki/Video-Streaming) after completing [Network Setup](https://github.com/themactep/thingino-firmware/wiki/Configuring-Wi%E2%80%90Fi-Access):

**a. Via RTSP:**
   - Thingino supports RTSP (Real-Time Streaming Protocol), allowing you to stream video from your camera to any RTSP-compatible player or software. The RTSP stream URL can be found in the camera's preview page after installation.

**b. Via Built-in Web-UI Preview Page:**
   - Thingino includes a built-in web interface that allows you to preview your camera’s video feed directly in a web browser in [MJPEG](https://en.wikipedia.org/wiki/Motion_JPEG) format. This is a quick and convenient way to check the camera's output without additional software, but it's more consumes more bandwidth and provides lower framerates than the H.264/H.265 streams provided via RTSP.  See the [[Web-UI|Web-UI]] entry for more information.

**c. Via ONVIF:**
   - For users integrating their camera into a larger security system, Thingino supports ONVIF (Open Network Video Interface Forum) protocol. This allows your camera to be detected and managed by ONVIF-compatible network video recorders (NVRs) and software.  It is enabled by default.

Once your device is up and running with Thingino, consider giving back to the community by [[contributing|Contributions]]. Whether it's through sharing your knowledge, improving the code, updating documentation, or simply spreading the word about Thingino, your contributions help make the project better for everyone. By getting involved, you can help shape the future of Thingino and support other users in their journey. Every contribution, no matter the size, makes a difference!