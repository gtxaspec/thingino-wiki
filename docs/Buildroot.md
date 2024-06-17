We use the latest available version of [Buildroot][1] with [slight modifications][2] that allow us to create a truly portable building environment.

## Cameras, Modules and Fragments

Camera hardware is primarily based on the SoC model, image sensor, and sometimes a wireless module. Different cameras may use the same SoC, sensor, and Wi-Fi module, thus requiring similarly built firmware, but still have different GPIO mapping and peripheral configuration. To avoid repeating settings in configs, we have decoupled camera-specific configs from the underlying hardware configs (we call them modules). We just tell the camera config stored in `config/cameras/' which hardware module stored in `config/modules/' to use:

```
# MODULE: t31x_gc2053_rtl8189ftv_defconfig
```

Then in the module config file we have everything configured for the Triade: SoC, sensor and the Wi-Fi module, if there is one.

But these hardware configs have a lot of common, repetitive information related to processor architecture and firmware in general. We use configuration fragments, stored in `config/fragments/*.fragment' files, to avoid repeating these settings. You can see how these fragments are included in the module config:

```
# FRAG: soc toolchain ccache brand rootfs kernel system target
```

This allows us to minimize the configuration steps required to add new hardware. And, if necessary, we can easily propagate changes to all dependent hardware.

## Config for compilation

When `make` is run, the final configuration for a given camera is assembled from the pieces and saved as a `~/output/<camera_config_name>/.config` file. It then runs `make olddefconfig`, which parses the file, resolves any conflicts and redundancies, and creates a new fully populated `.config` file, saving the previous version as `.config.old`, which gets overwritten with any new changes, so we also save the initial version of the `.config` file as `.config_original` for easier debugging.

To recreate the `.config` file from the original camera configuration file and its includes, run `make defconfig`.

## local.fragment and local.mk

We provide a file for local changes to a shared configuration. The `config/fragments/local.fragment` file can contain settings that should be included in a common config on the developer's machine, but don't go into the upstream repository. You can add additional packages there or override the default settings:

```
BR2_PACKAGE_NANO=y
BR2_PACKAGE_SCREEN=y
BR2_REPRODUCIBLE=n
```

The `local.mk` file placed in the root of the firmware directory is a standard Buildroot feature that allows you to override package sources, including those from the Buildroot itself. This is an invaluable feature for local development. Read more about this in chapter 8.13.6 of <https://buildroot.org/downloads/manual/manual.html>.

```
LINUX_OVERRIDE_SRCDIR=$(HOME)/dev/thingino/linux
LINUX_HEADERS_OVERRIDE_SRCDIR=$(HOME)/dev/thingino/linux
INGENIC_SDK_OVERRIDE_SRCDIR=$(HOME)/dev/thingino/ingenic-sdk
PRUDYNT_T_OVERRIDE_SRCDIR=$(HOME)/dev/thingino/prudynt-t
```

[1]: https://buildroot.org/
[2]: https://github.com/buildroot/buildroot/compare/master...themactep:buildroot:master