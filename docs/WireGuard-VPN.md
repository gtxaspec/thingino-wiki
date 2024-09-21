Thingino includes support for the [WireGuard](https://www.wireguard.com/) VPN protocol.

It may be desirable - in the case of remote cameras on untrusted networks, for example - to establish a secure connection to some central collector. While Linux and WireGuard support complicated routing configurations, this interface supports the simple use case of connecting a single tunnel to a peer (server), and routing traffic from the camera, to a set of CIDRs (networks) through that server.

## Configuration
The following persistent environment variables are used:

* `wg_address` - the address and mask length of the wireguard interface, eg. `192.0.2.1/24`
* `wg_allowed` - a list of networks to be routed through the tunnel
* `wg_enabled` - set to `true` to enable WireGuard at boot.
* `wg_endpoint` - the WireGuard server, eg. "vpn.example.com:51280"
* `wg_peerpub` - the public key of the WireGuard server
* `wg_privkey` - the private key of this camera
* `wg_dns` - (optional) a list of DNS resolvers to use when the VPN is up, eg. `192.0.2.254`
* `wg_keepalive` - (optional) the interval at which keep-alive messages are sent. This is likely unnecessary if an RTSP stream is connected to a client (eg. frigate, zoneminder, mpv, ffplay,...)
* `wg_mtu` - (optional) the maximum transmission unit. It is likely unnecessary to change this from the default value of 1420.
* `wg_peerpsk` - (optional) WireGuard can use an additional preshared key for additional protection.
* `wg_port` - (optional) the local listening port for this instance. It is likely unnecessary to set this

These variables should be considered as reserved and not used for any other purpose.

Lists of addresses, networks, or CIDRs may be separated by commas or spaces; `192.0.2.1,192.0.2.2`, `192.0.2.1, 192.0.2.2`, or `192.0.2.1 192.0.2.2` are all valid.

## WebUI

There is a panel in the WebUI for configuring the WireGuard subsystem; it can display the configuration variables as stored in the firmware environment, and allows those variable to be set. The correct values are site-specific and can be obtained from the WireGuard server, the exact details of the process depend on the server (eg. OpenWRT, vendor-skinned OpenWRT, pfSense, OpnSense).

The panel can also display the state of the tunnel if the interface is up, and allows the VPN to be started or stopped on demand.

![wg_gui2](https://github.com/user-attachments/assets/ac77a78c-0380-40a1-9e68-4b9ef37d064a)

Once WireGuard has been configured, reboot the camera to apply the changes or use the red button to start or stop the VPN immediately. Use caution when configuring remote devices as VPN changes may lead to loss of connectivity.

## CLI

If desired, the environment variables can be set with `fw_setenv`. To protect flash lifetime, it is recommended to use the bulk/script mode of fw_setenv. For example, create `/tmp/wg_env.txt` with the following contents and load them with `fw_setenv -s /tmp/wg_env.txt`.

```
wg_enabled false
wg_keepalive 25
wg_endpoint vpn.example.com:51280
wg_mtu 1420
wg_dns 192.0.2.253
wg_address 192.0.2.1/32
wg_allowed 192.0.2.0/24, 195.51.100.0/24
wg_peerpub QQQQQQQQQQQQQQQQQQQQQQQQQQQQQQQQQQQQQQQQQQQ=
wg_privkey XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX=
wg_peerpsk ZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZ=
```

The VPN can then be immediately started with `/etc/init.d/S42wireguard force`. If that works, the `wg_enabled` flag can be set to `true` to enable autostart. If you're confident in your VPN configuration create the environment with `wg_enabled true` and reboot - may the odds be ever in your favor.

