The [Wyze Doorbell V1](https://www.wyze.com/products/wyze-doorbell) comes with a Chime that can be plugged into an outlet.  The camera and the chime communicate via the Sub1GHz band at 906.4 MHz using GFSK. See [FCC ID 2AUIUWDBC1A](https://fcc.report/FCC-ID/2AUIUWDBC1A/5922685).
The encoding is not readily decoded with either Flipper Zero (Official firmware or Unleashed) or rtl_433.

The doorbell camera uses a [CC1310](https://www.ti.com/product/CC1310) chip that combines MCU + Radio. It appears as serial device `/dev/ttyS0` in the camera.  Writing to/reading from this device sends commands to the chime.

Each chime has a 4-digit MAC that's printed on the back, such as `77:D8:FD:53`.

## Executive Summary.
During pairing, the camera issues a number of commands. First, the camera must discover the chime's MAC address.
Once it has that, it will send a challenge to the chime. The chime responds with a code that's validated via Wyze's APIs.
Once validated, the camera sends VERIFY_RESULT to the chime to complete the process.  
It is not clear whether the Chime's MCU cryptographically checks the result, or whether this is solely to
keep track of which chime is connected to which camera.

## Use with Thingino

An already paired chime can be used with Thingino as follows

- Turn on power to the transceiver by setting GPIO 61 high:
```
gpio high 61
```
- Put `/dev/ttyS0` in raw mode and 115200 baud
```
stty -F /dev/ttyS0 raw
stty -F /dev/ttyS0 speed 115200
```
- You can now send sounds. (the `SUB1G_INIT` command below appears to not be necessary.)

## Message Format
The communication protocol appears to be as follows.  
```
AA 55 53   - all commands from camera to chime start with this header
LEN        - if this value is < 0x70, it denotes the length of the remainder of the packet, not including LEN but including the cksum.
             See below for an exception.
CMD        - this byte appears to be the command code.  It determines the format of what follows.
[BODY]     - a variable number of bytes depending on CMD
CHK1 CHK2  - two bytes for a checksum. That's the simple 16-bit sum of all preceding bytes, including the AA 55 53 header. Big Endia
```

### Example Packet
An example packet is:
`0xaa 0x55 0x53 0x03 0x3f 0x01 0x94`
where the CMD is 0x3f (nothing follows this command)
`hex(0xaa+0x55+0x53+0x03+0x3f)` is 0x194. The LEN is 0x3 in this case.

### Command Codes

Below is a list of identified command codes and their suspected meaning.

#### SUB1G_INIT

CMD is `0x14` and it is followed by a single `0xff` in the body. 
This is issued when the camera starts up. It appears to initialize the CC1310.
Full packet: `0xaa 0x55 0x53 0x04 0x14 0xff 0x02 0x69`

#### SUB1G_DELETE_ALL_CHIME

CMD is 0x3f.  Empty body. We suspect it's issued to deassociate all chimes.

#### PAIRING

CMD 0x1c

This is followed by either 0x1 or 0x0 in the body.

- `0x1c 0x01` is issued when the pairing process is started.

  The camera appears to send PAIRING with `0x1c 0x01` to start the pairing process. If the chime is put in pairing mode, 
  the camera should receive a reply with the chime's MAC.  Reply packets start with `0x55 0xaa x53`. The camera will then
  send a response contained its MAC, see below.

- `0x1c 0x00` is issued to stop the pairing process

#### RANDOM_DATE_SEND

CMD 0x21

This is sent next during the pairing process.
The BODY is:
```
8 bytes MAC address encoded as one hex byte per ASCII char, so `77:D8:FD:53` becomes `0x37 0x37 0x44 0x38 0x46 0x44 0x35 0x33`
16 bytes of what appears to be a randomly produced seed
```

The chime will respond with a message with response code `0x22` along with its MAC address and a so-called "R string" that is then sent to Wyze's API servers.

#### VERIFY_RESULT

CMD 0x23

Once the API server responded successfully, the camera will send this to the chime to complete the setup process.

BODY: 
```
8 bytes MAC address of chime
FF 04
```

#### GET_DONGLE_VERSION

CMD 0x16

Empty body.  Presumably a request to send a version back to the camera

#### PLAY

This code actually plays a chime. There appear to be 2 codes that do that identically.

CMD 0x70
CMD 0x47

BODY
```
8 byte of MAC address for CHIME
SOUNDID
REPEAT
VOLUME
```

The SOUND Id is a one byte number denoting the chime in the order they are listed in the app, from 1 being "space wave" to 19 being "Intruder". REPEAT is set 1 to play it once, 2 twice, and so on.
VOLUME is 1 and up.

## Response Message format

The format of messages from the chime to the camera appears to be similar. Here is an example that is sent when the Chime is ready to pair
```
RcvData:                                                                               |
0x55 0xaa 0x53 0x0e 0x20 0xa3 0x37 0x37 
0x44 0x38 0x46 0x44 0x35 0x33 0x0c 0x15
0x04 0x20 
```
Format
```
55 AA 53           - 3 byte header
LEN                - like in other direction
RES                - response code
[BODY]
CHKSUM
```

RES = 0x20 appears to be a confirmation to pair, in this case, the body contains the MAC address of the chime along with other
information:
```
0x55 0xaa 0x53 0x0e 0x20 0xa3 0x37 0x37 0x44 0x38 0x46 0x44 0x35 0x33 0x0c 0x15 0x04 0x20
               LEN   RES   ??    7    7    D    8    F    D    5    3   ??   ??  CKSUM    
```

### Exception.

Special case: we have observed one packet where the fourth byte is not the length. 

```
0xaa 0x55 0x53 0x71 0xff 0x02 0xc2
```
here `0x71 0xff` replaces LEN + CMD + BODY.
This is sent in response to a packet from the chime that's `0x55 0xaa 0x53 0x70 0xff 0x02 0xc1`
Perhaps this is a heartbeat?

