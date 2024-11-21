# Remote Access in Thingino

Thingino offers several methods to enable remote access to your system, making it easy to control your device from anywhere. Here’s an overview of the available options:

## 1. **VPN Access with WireGuard**
WireGuard is built into Thingino, providing an easy-to-setup VPN solution right out of the box. By using WireGuard, you can securely connect to your Thingino device over the internet, ensuring privacy and safety. 

## 2. **ZeroTier or Tailscale**
If you prefer using other VPN options, you can compile your own version of Thingino to include **ZeroTier** or **Tailscale**. Both services are excellent alternatives that offer seamless, private connections over the internet. You will need to include ZeroTier or Tailscale in your custom Thingino build.

## 3. **IPv6**
If your Internet Service Provider (ISP) supports IPv6, you can use it to connect directly to your device over the internet. Simply unblock the desired port on your router, and you’ll be able to access your Thingino system using its IPv6 address. Open the port you want to access remotely and use your device’s IPv6 address.

## 4. **WebRTC via External Helper Programs (e.g., Go2RTC)**
WebRTC allows you to connect with your Thingino device via a browser without the need for plugins. You can use an external helper program, such as **Go2RTC**, to enable external WebRTC support on Thingino, without needing to modify any router configuration.

## 5. **Home Assistant and Other Integrations (e.g., Frigate)**
You can also integrate Thingino with smart home platforms such as **Home Assistant** or other applications like **Frigate**. These platforms allow you to remotely monitor and control your Thingino device with user-friendly interfaces.

## 6. **Mobile Access via Apps (e.g., TinyCam)**
Once you have set up any of the above remote access methods, you can also use mobile apps such as **TinyCam** to view and control your Thingino device from your smartphone or tablet. TinyCam is a popular app that supports many IP cameras and provides an easy way to remotely monitor your device on the go. 

---

There are many guides available to help configure the various methods described above. Searching the web for setup instructions is a great way to find the resources you need to get started and make the most out of your remote access configuration.