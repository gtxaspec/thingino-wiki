Hardware
--------

There are several versions of the popular, inexpensive, and versatile 24/25 series EEPROM programmer.

![image](https://github.com/user-attachments/assets/ab1b6cb5-cccd-44a4-b933-a4b457d69084)
![image](https://github.com/user-attachments/assets/e2baee8d-3608-408d-b7a2-e13c5eef96c3)
![image](https://github.com/user-attachments/assets/a3c8fb22-236b-4282-9b92-2dad08301850)
![image](https://github.com/user-attachments/assets/9282a191-ab3b-4426-a9d5-a32a7c8d57dd)

Older model, the black one with the gold edge (rarely green with a silver edge), is the cheapest. But it has a nasty hardware quirk which [must be fixed](#fixing-higher-than-needed-dataline-voltage-bug) before you can use the programmer with any 3.3V flash chip.

[![CH341A programmer](https://img.youtube.com/vi/qXLmrmb0BJc/0.jpg)](https://youtu.be/qXLmrmb0BJc)


Software
--------

I prefer [this fork of SNANDer](https://github.com/Droid-MAX/SNANDer), but there is also

- Original [SNANDer](https://github.com/McMCCRU/SNANDer)
- [microsnander](https://github.com/OpenIPC/microsnander) from OpenIPC
- [ch341prog](https://github.com/setarcos/ch341prog/)
- [flashrom](https://www.flashrom.org/Flashrom)


Working with a clip
-------------------

The programming clip allows you to read and write the contents of the flash memory chip without having to desolder the chip.

Connect the clip to the CH341A programmer using a DIP8 adapter and gently pinch the chip with the clip jaws. In your computer, run `snander -i` and confirm the chip is detected.

### Reading the firmware

Use `snander -r <filename>` to save a copy of the flash chip content to a file.

Repeat the procedure of reading twice back to back using different filenames. Then compare checksums of these files.

```
md5sum <filename1> <filename2>
```

If the checksums match, the firmware is saved correctly. If they don't, check your setup and repeat the process  until you get two identical files.

### Writing the firmware

Use `snander -e && snander -w <filename> -v` to erase the flash chip clean and write a new firmware to it with verification of the result.

Tutorials
---------

Programming Jooan A6M with a clip, part 1

[![Programming Jooan A6M with a clip, part 1](https://img.youtube.com/vi/lDzk7r3xyGE/0.jpg)](https://youtu.be/lDzk7r3xyGE)


Programming Jooan A6M with a clip, part 2

[![Programming Jooan A6M with a clip, part 2](https://img.youtube.com/vi/zWBrI0DF35U/0.jpg)](https://youtu.be/zWBrI0DF35U)



Troubleshooting
---------------

To make the CH341A work on a Raspberry PI, you must add these to `/boot/cmdline.txt`:

```
dwc_otg.fiq_enable=0 dwc_otg.fiq_fsm_enable=0
```

Fixing higher than needed dataline voltage bug
----------------------------------------------

Early versions, prior to version 1.7, of the cheap and popular CH341A mini programmer have a nasty bug where the voltage levels on the data lines remain at 5V even though the programmer is jumpered to 3.3V.

[@ddemos1963](https://github.com/ddemos1963) came up with an interesting hack to solve the problem in an efficient and artistic way.

![image](https://github.com/user-attachments/assets/ddcda912-a332-4c03-b932-3951328ea27e)
![image](https://github.com/user-attachments/assets/d5c94b52-d9e2-4873-aec9-e2032d77902a)

Here's what you need to do.

![image](https://github.com/user-attachments/assets/ccdbd6a6-42df-490f-ade3-c4fd74a6b882)

Sever the connection between the 5V power line and the CH341A chip. Use a sharp utility knife to cut the trace on the backside of the programmer board.

![image](https://github.com/user-attachments/assets/c370fa1e-b698-44af-a4cc-cd05857f0fbb)

Connect the 3.3V output leg of the voltage regulator to pin 9 of the CH341A IC by bridging it to a corresponding trace at the capacitor located nearby.

![image](https://github.com/user-attachments/assets/a506573c-94ff-4150-b559-2728877d3ba0)

Restore power to the chip by re-routing the 3.3V voltage from the 3v3 pin to pin 28 of the CH341A IC through the 5V pin connector on the header.

![image](https://github.com/user-attachments/assets/310e4b82-d7ac-4e03-a6fc-9222b21d6108)


Resources
---------

- [DIY BCQ CH341A forum](http://www.diybcq.com/thread-144131-1-1.html) (Chinese, use Chrome automatic translation)
- [CH341A Programmer](https://4pda.to/forum/index.php?showtopic=884713) (Russian, use Chrome automatic translation)
