> [!WARNING]
> Thingino is a DIY project that may require disassembly and some advanced computer skills. While the developers strive to ensure that all procedures and software are safe, reliable, and as user-friendly as possible, users should be prepared for the technical nature of the project. **Please note that Thingino is under heavy, constant development and is still early in its lifecycle, so some features may be in the early stages of development.** It’s important to be aware that, in rare cases, unforeseen circumstances could lead to device damage or corruption. As such, users should proceed with caution and be prepared for potential challenges.

### Introduction to Thingino

Welcome to Thingino! Thingino is designed to help you get the most out of your devices. At its core, Thingino involves replacing your device's original factory firmware—essentially its operating system—with our custom-built firmware. This process unlocks new features, improves performance, and gives you greater control over how your device functions.

In simple terms, you'll be erasing the manufacturer's software and installing Thingino instead. While this might sound a bit intimidating, we've created detailed guides and tools to make the process as straightforward as possible, even for those new to this kind of project. Our goal is to empower you to customize your device safely, reliably, and easily.

If you're ready to dive in, you'll find great information throughout our wiki. Let's get started on transforming your device with Thingino!

### Thingino and Linux: What You Need to Know

Thingino is built on the Linux operating system. This means that installing and working with Thingino requires a foundational understanding of Linux. Basic Linux skills, such as navigating the command line, understanding file system structure, and performing simple commands, are essential for a successful installation and smooth operation of your Thingino device. If you're new to Linux, don’t worry—there are plenty of helpful guides available on the web that can help you get up to speed before you begin.

Mastering these basic Linux skills will not only help you install Thingino but also empower you to fully harness its capabilities, giving you greater control and customization options for your device.

### How to Choose a Compatible Device for Thingino

When selecting a device to use with Thingino, consider the following factors:

**a. Device Type:**  
   - Thingino supports a variety of devices, including indoor and outdoor cameras, fixed-angle and PTZ (Pan-Tilt-Zoom) models, and smart doorbell cameras. Whether you need a basic indoor camera, a weatherproof outdoor model, or advanced PTZ functionality, Thingino offers compatibility with a wide range of devices for various use cases.

**b. Confirmed Working Devices:**
   - Visit [Thingino.com](https://thingino.com) for a list of devices that have been thoroughly tested and confirmed to work with Thingino. This list is regularly updated based on community feedback and internal testing.

**c. Choosing Your Own Ingenic-Based Device:**
   - If you choose to use a device that isn’t listed on Thingino.com, ensure it features an Ingenic SoC, as Thingino will work only on cameras that use Ingenic-based SoCs that power many affordable IP cameras. Before making a purchase, review the device’s specifications (if possible) or consult the [[community|Resources-and-Links#information]] to verify compatibility with our [[supported hardware|Tech-Info-‐-Supported-Hardware]]. Be prepared to undertake tasks such as disassembling the device, photographing and documenting the PCB, [[connecting to UART ports|UART-Connection]] to access boot logs, and dumping the firmware. For detailed instructions, refer to the [[porting guide.|Porting-Guide]]

**d. Performance Specifications:**
   - We recommend selecting a device with an Ingenic X series SoC, such as the T20X, T30X, or T31X/ZX/A, because these SoCs come equipped with 128MB of onboard RAM. Additionally, look for a device with a flash chip of at least 16MB, as this will enhance the device’s longevity. Insufficient RAM can lead to performance limitations, and low storage capacity will severely restrict the addition of new features.

### Determining How to Install Thingino

> [!WARNING]  
> We **strongly recommend** creating a **full backup** of the existing stock firmware. This is an essential step if you ever need to restore the original functionality or analyze the stock firmware for compatibility.

Once you have your device, there are several methods to create a full backup and then install Thingino depending on your device's capabilities:

**a. Install Using USB (If USB Data Works):**
   - If your device supports USB data transfer, you can backup and then install Thingino directly via USB. This is often the simplest method, requiring minimal technical knowledge. At a minimum, this may require disassembly, but not modification of the device. Follow the detailed [Ingenic USB Cloner](https://github.com/themactep/thingino-firmware/wiki/Ingenic-USB-Cloner) guide available in the wiki. 
   - Note that the usb cords included with cameras typically do not have data lines, you will need to provide your own tested cord. Also note that the presence of a USB port on the camera does not necessarily mean that USB data transfer is possible on the camera; the port may be used just to power the camera.

**b. Install via No-Tool Installation:**
   - Some devices support a [no-tool installation](https://github.com/themactep/thingino-firmware/wiki/No-Tool-Installation) method, allowing you to flash Thingino without any special hardware tools. This method is ideal for users who want a straightforward installation process, with no device disassembly required. Device specific instructions can be found in the wiki.

**c. Install via Flash Chip Programmer:**
   - For advanced users, or if other installation methods are not feasible, you can use a [flash chip programmer](https://github.com/themactep/wiki/blob/master/hacking/ch341a-programmer.md) to backup and then install Thingino. This method requires disassembling the device and connecting a programmer to the device's flash chip. It’s recommended for users with experience in hardware programming.

**d. Install via U-Boot/SD-Card:**
   - Some cameras can be flashed via SD Card from the stock UBoot bootloader prompt.  This method requires that you access and then
    interrupt the stock firmware's boot process via the [[UART console|Installation#from-an-sd-card]], load the image from the SD Card, and
    flash it via UBoot's flash write commands.

### Initial Setup After Installing Thingino
After you get the Thingino firmware installed on your camera, you should see a new WiFi access point.  
* Use your phone/laptop/etc and view the available wireless networks.  Your camera will show up as an access point before you configure it to connect to your wireless network.
* Connect to the WiFi network that looks something like `THINGINO-xxxx`
* Congratulations, the installation was successful! Now continue to the [Configuring WiFi Access](https://github.com/themactep/thingino-firmware/wiki/Configuring-Wi%E2%80%90Fi-Access#captive-portal) wiki article to get the new camera on your wireless network.


### Accessing Your Camera Running Thingino

After successfully installing Thingino and completing network setup, you can access your camera through various methods:

- **Default Credentials**: `root/root`

#### Accessing via Web UI

- **Hostname**: `http://hostname.local`
- **IP Address**: `http://192.168.1.100` (replace with your actual IP address)

For detailed instructions on using the Web UI, see the [[Web UI|Web-UI]] article.

#### Accessing via SSH

For advanced configuration, connect via SSH:
- **SSH Access**: `ssh root@192.168.1.100` (replace with your device’s IP address)

#### Accessing via RTSP

- **RTSP Stream URL**: Found on the camera's preview page after installation. RTSP provides better performance and lower bandwidth usage. 
 
  - See the [[Video Streaming Endpoints|Video-Streaming]] article for more information.

#### Accessing via Built-in Web-UI Preview Page

- **Preview Page**: Allows you to view the camera feed in MJPEG format directly in a web browser. Note that this method provides lower framerates compared to RTSP.
  - See the [[Web UI|Web-UI]] article for more information.

#### Accessing via ONVIF

- **ONVIF Support**: Enables integration with ONVIF-compatible NVRs and software. This feature is enabled by default.

Once your device is up and running with Thingino, consider giving back to the community by [[contributing|Contributions]]. Whether it's through sharing your knowledge, improving the code, updating documentation, or simply spreading the word about Thingino, your contributions help make the project better for everyone. By getting involved, you can help shape the future of Thingino and support other users in their journey. Every contribution, no matter the size, makes a difference!

### Updating Thingino Firmware

To update your Thingino device, you can use the `sysupgrade` command directly from the device via SSH:

- **Partial upgrade (recommended)**: Preserves settings like Wi-Fi and passwords.
  ```bash
  sysupgrade -p
  ```

- **Full upgrade**: Resets the device, including bootloader and settings.
  ```bash
  sysupgrade -f
  ```

For more details on updating, visit the [Updating Firmware](https://github.com/themactep/thingino-firmware/wiki/Updating-Firmware) article in the wiki.
