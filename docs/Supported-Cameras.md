Please visit <http://thingino.com/> for the list of supported cameras.

If you have a camera that works with Thingino and you'd like to add it to the list of supported cameras, please submit a pull request to this repository.

If you have a camera in mind that you would like to make work with Thingino, but do not have the [skills to do it yourself](Porting-Guide), please consider donating a copy of such a camera to the project.  

You may also view the complete table of [Supported Hardware](https://github.com/themactep/thingino-firmware/wiki/Tech-Info-%E2%80%90-Supported-Hardware).

---

### Secure Boot and Camera SoC Security

#### Overview

Some camera brands use a security method to protect their devices by embedding a secret key into the System on Chip (SoC). This key ensures that only vendor authorized firmware can run on the camera.

#### How It Works

1. **Secret Key in OTP Area**: During manufacturing, a unique secret key is written into the One-Time Programmable (OTP) area of the device's SoC. This key cannot be changed once it is set, it's an irreversible process.

2. **Firmware Signing**: The device's firmware is digitally signed by the manufacturer using a key that matches the secret key stored in the OTP area.  Only the vendor has this secret key.

3. **Verification Process**: When the device boots up, it checks the firmware's digital signature using the OTP key. If the firmware is signed correctly, the device will boot. If not, the device will not start, rendering it unusable.  Without the secret key, new firmware can not be created to use on the device.

#### Implications

1. **Firmware Restrictions**: Only firmware signed by the manufacturer can be installed and run on the device. Any other firmware will cause the device to fail to boot.

2. **Boot Failures**: If you try to install firmware that is not signed with the correct key, the device will not work. 

3. **Physical SoC Replacement**: The only way to fix the device is to replace the SoC chip with a new one. This is because the OTP key cannot be modified or reset.  This involves using specialized equipment to physically remove and replace the SoC chip. thingino.com lists these as "Conditionally Supported"