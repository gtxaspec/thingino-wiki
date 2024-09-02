## Updating Thingino Firmware

The `sysupgrade` command is the primary method for updating your Thingino device's firmware. This command allows you to perform either a full or partial upgrade of the system, depending on your needs. Below is a guide on how to use this command effectively.

### Basic Usage

To use the `sysupgrade` command, you can run it with one of the following options:

```sh
sysupgrade <filename> | [-f | -p] | <URL>
```

### Options

- **`-f`**: Perform a full upgrade. This option upgrades the entire system, including the bootloader. It is the most thorough update method but will reset the U-Boot environment, which includes settings like your Wi-Fi SSID, password, and root password.
  
- **`-p`**: Perform a partial upgrade. This is the recommended option for most users as it upgrades the system while preserving the U-Boot environment. Your Wi-Fi SSID, password, and root password will remain intact.

- **`<filename>`**: Perform a full or partial upgrade using a local file. This option is useful if you have already downloaded the firmware binary and want to upgrade without fetching it from a remote source.

- **`<URL>`**: Perform a full or partial upgrade using a URL. This option allows you to specify a direct URL to the firmware binary for the upgrade.

- **`-h`**: Display help information for the `sysupgrade` command.

### Recommendations

- **Partial Upgrade (`-p`)**: This option is recommended for most users as it preserves critical settings such as the U-Boot environment. Use this option to upgrade your system while keeping your Wi-Fi credentials and root password unchanged.

- **Full Upgrade (`-f`)**: Use this option only when you need to perform a complete system overhaul, including the bootloader. Be aware that this will reset your U-Boot environment, so you may need to reconfigure your Wi-Fi and other settings afterward.

### How It Works

The `sysupgrade` script will automatically download the latest precompiled build for your specific device from the Thingino GitHub repository. Whether you choose a full or partial upgrade, the script ensures that you are running the latest available firmware for your device.

### Example Commands

1. **Partial Upgrade (recommended):**
   ```sh
   sysupgrade -p
   ```
   This command will fetch the latest partial upgrade from the GitHub repository and apply it, preserving your U-Boot environment.

2. **Full Upgrade:**
   ```sh
   sysupgrade -f
   ```
   This command will perform a complete system upgrade, including the bootloader. Use this only when necessary, as it will reset your U-Boot environment.

3. **Upgrade from a Local File:**
   ```sh
   sysupgrade /path/to/firmware.bin
   ```
   Replace `/path/to/firmware.bin` with the actual path to your firmware file. This command will perform the upgrade using the specified file.

4. **Upgrade from a URL:**
   ```sh
   sysupgrade https://example.com/firmware.bin
   ```
   Replace `https://example.com/firmware.bin` with the actual URL of the firmware binary. This command will download the firmware from the URL and perform the upgrade.

Updating your Thingino device is straightforward with the `sysupgrade` command. Most users will find the `-p` option sufficient for keeping their device up to date while preserving their settings. Reserve the `-f` option for situations where a complete system update, including the bootloader, is required.