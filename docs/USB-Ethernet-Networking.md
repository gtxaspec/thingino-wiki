**Thingino** supports USB networking out of the box, making it easy to connect and configure network adapters for various devices. Here's some quick information on using USB networking with Thingino and the types of adapters supported.

#### Supported USB Adapters

Thingino provides built-in support for several USB networking adapters. The following types of adapters are supported out of the box:

- **ASIX AX88772-based USB adapters**: These are well-supported and should work seamlessly with Thingino.
- **CDC-Ethernet networking adapters**: Many Ethernet adapters that support CDC-Ethernet are also fully compatible with Thingino.

The necessary drivers for these adapters are pre-enabled in all Thingino builds for devices that support USB OTG data, meaning there is no need for manual driver installation or configuration.

#### Using USB Networking

To use a USB network adapter with Thingino, simply plug it into the device. The ethernet adapter should be recognized automatically if it's one of the supported types. You can then proceed to configure the network settings, or in many cases, the connection will work out of the box.

#### Important Note on Compatibility

While most adapters work well, some devices may encounter issues due to hardware limitations, particularly the USB ports. One notable example is the **WYZE Cam V3**, where the micro USB socket has been known to wear out easily over time.

**Potential issues with WYZE Cam V3**:
- Micro USB ports on this model can degrade with repeated use, leading to unreliable connections.
- Some OTG adapters or Ethernet adapters with micro USB connectors may exhibit connectivity issues or generate errors when plugged into a worn socket.
- These problems are not due to the adapter or Thingino but are a result of physical wear on the WYZE camera's USB socket.

---

For reliable USB networking on Thingino, ASIX AX88772-based adapters and CDC-Ethernet adapters are highly recommended. Be aware of potential hardware issues on devices like the WYZE Cam V3, where micro USB sockets can become worn and cause connectivity problems.
