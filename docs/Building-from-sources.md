## Prerequisites

To successfully compile the firmware, you need a modern Linux distribution equipped with up-to-date system libraries and tools. Specifically:

> [!IMPORTANT]  
> Building is currently supported only on **x86_64** platforms. Attempting to build on RISC-V or ARM64 hosts will result in failure.

- **Required Distribution**: Recent versions of Debian or Ubuntu, are recommended.
- **Essential Libraries and Tools**:
  - **glibc 2.31 or newer**: Ensure your system's C library is up-to-date to avoid compatibility issues.
  - **GNU awk**: Required for processing scripts during the build.

If you are using an older operating system or prefer not to install additional packages on your existing system, consider using **Podman**, **Docker** or **LXC** containers. These provide a clean and isolated environment, ideal for ensuring compatibility and replicability of the build process.

For detailed instructions on setting up and using containers to compile firmware, visit our [Container Development page](https://github.com/themactep/thingino-firmware/wiki/Development#containers).

## Downloading the repository

### Step 1: Clone the Repository

Start by cloning the Thingino firmware repository to your local machine. Open a terminal and run the following command:

```bash
git clone --depth=1 --recurse-submodules \
--shallow-submodules https://github.com/themactep/thingino-firmware
```

### Step 2: Navigate to the Firmware Directory

Change into the cloned directory:

```bash
cd thingino-firmware
```

## Guided Compilation

### Step 1: Launch the Configuration Menu

Run the user configuration script:

```bash
./user-menu.sh
```

Upon running the script, you will see the main menu:

![image](https://github.com/themactep/thingino-firmware/assets/12115272/ec95798b-2b1c-44c7-b0fe-d27f5809a7c9)

Select **"Guided Compilation"** from the menu.

![image](https://github.com/themactep/thingino-firmware/assets/12115272/98997b30-847b-4b4d-89ce-a3682aec636b)

### Step 2: Select Your Device Profile

1. **Select Device**: Choose a device profile from the list. You can select either a **Camera Profile** or a **Module Profile**:
   - **Camera Profile**: Includes all necessary configurations for the device, such as GPIOs.
   - **Module Profile**: Basic configuration suitable for experienced developers.

![image](https://github.com/themactep/thingino-firmware/assets/12115272/d1fb2108-b001-4fea-a754-f88f767d2351)

Click **OK** to confirm your selection.

### Step 3: Install Prerequisites

Select **"Install prerequisites"** from the menu to install the necessary components for compilation.

![image](https://github.com/themactep/thingino-firmware/assets/12115272/d04e3196-c33f-404a-b7e2-217473486585)

### Step 4: Compile the Firmware

Select **"Step 3: Make Firmware"** to start the compilation process.

![image](https://github.com/themactep/thingino-firmware/assets/12115272/542d8b95-b18f-43db-b4ec-b458a60b19d8)

Please wait while the firmware compiles; this may take some time. This step also creates the necessary images to flash the firmware onto your device.

### Step 5: Retrieving the Compiled Firmware

![image](https://github.com/themactep/thingino-firmware/assets/12115272/be4a8911-9dfc-4659-9a1a-60bc985f4f30)

Upon completion, a message will indicate that the process is done. You can find the firmware images in your home directory under:

```
HOME FOLDER/output/<profile_name>/images
```

For example:
- `thingino-teacup.bin` – This full image includes the bootloader and is used for fresh installations.
- `thingino-teacup-update.bin` – This image does not include the bootloader and is suitable for updating your device without erasing your bootloader or environment variables.

### Conclusion

Congratulations! You have successfully compiled and prepared the Thingino firmware for installation. Follow the above steps to recompile or update the firmware as needed.

## Manual Compilation

- Run `make` and select a device profile. 
- Upon completion, a message will indicate that the process is done. You can find the firmware images in your home directory under:

```
HOME FOLDER/output/<profile_name>/images
```

For example:
- `thingino-teacup.bin` – This full image includes the bootloader and is used for fresh installations.
- `thingino-teacup-update.bin` – This image does not include the bootloader and is suitable for updating your device without erasing your bootloader or environment variables.