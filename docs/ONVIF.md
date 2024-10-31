ONVIF protocol in Thingino is handled by [onvif_simple_server](https://github.com/roleoroleo/onvif_simple_server) by @roleo.

The server consists of three components:

- **wsd_simple_server**, a daemon that replies to discovery on port 3702.
- **onvif_notify_server**, a daemon that handles events, if enabled.
- **onvif_simple_server**, handles all other responses. This one is a CGI application, not a daemon.

### Configuration

The `/etc/onvif.conf` configuration file is generated during firmware compilation to contain information specific to the actual hardware and firmware. It is preset to handle most cases, but can be further customized to meet specific needs.

### Development

Test the server with the "official" ONVIF tools:

- [ONVIF Device Manager](https://www.help.onvif.org/index.php?/selfhelp/view-article/onvif-device-manager)
- [ONVIF Device Test Tool](https://github.com/onvif/testspecs/discussions/7)

### Debugging

**To debugging ONVIF**

Run

```
echo 5 > /tmp/onvif.debug
```

Three last calls will be saved to `/tmp/onvif.log`

**To debug WSD daemon**

Add `-d 5` to its command line then check `/tmp/wsd.log` file for debug ouput.


### Links

Further details available here:
https://github.com/roleoroleo/onvif_simple_server/blob/master/README.md

