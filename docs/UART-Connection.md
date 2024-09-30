Open the camera case.

Get a [USB to TTL UART adapter][1].

__Before you connect that adapter to you camera, make sure that it's working voltage is set to 3.3 volt!__

Connect ground (GND) contact on the adapter to ground contact on the camera.

Connect RX contact of the adapter to TX contact of the camera.

Connect TX contact of the adapter to RX contact of the camera.

**Do not connect VCC contact!** Power the camera with its standard power adapter.

Set your terminal settings to 115,200 bps baudrate, 8 bits, no parity, 1 stopbit, no flow control. You should start seeing booting log in your terminal window.


### Commands for various terminal programs with session logging

#### screen

```bash
screen -L -Logfile ipcam-$(date +%s).log /dev/ttyUSB0 115200
```

Use `Ctrl-a` followed by `\` to exit the session.

#### `minicom`

```bash
minicom -b 115200 -8 --capturefile=ipcam-$(date +%s).log --color=on -D /dev/ttyUSB0
```

Use `Ctrl-a` followed by `x` to exit the session.

#### `picocom`

```bash
picocom -b 115200 --databits 8 --parity n --stopbits 1 --flow n --logfile=ipcam-$(date +%s).log /dev/ttyUSB0
```

Use `Ctrl-a` followed by `Ctrl-x` to exit the session.

#### PuTTY

If you opt for a GUI terminal, namely [PuTTY](https://www.putty.org/), this is how it should look like:

![PuTTY settings screen](https://user-images.githubusercontent.com/29582865/207894192-c6f66401-7715-4aa6-bee2-8343aae6c0a9.png)
![PuTTY connection screen](https://user-images.githubusercontent.com/29582865/209340268-e34a010c-d455-4343-ae83-0866f0f0af15.png)

[1]: https://www.aliexpress.com/w/wholesale-usb-to-ttl-uart.html





Jooan A6M TX-RX Pinout:


![jooan-a6m](https://github.com/user-attachments/assets/af52c554-9f64-491a-becc-11c9ddad78d1)

![unknown-T23](https://github.com/user-attachments/assets/15669ca8-8995-410f-b9ca-9aded561fc45)
