## Buildroot

Thingino is an external tree of the [Buildroot][1] tool. So the best possible documentation is available [here][2].

Thingino uses a slightly [modified version][3] of Buildroot, allowing it to create better symlinks for a truly relocatable toolchain.

Thingino uses its own `Makefile` to do most of the pre-build configuration. It then passes the build command to Buildroot.

Buildroot's native `make` directives are accessible from firmware using the `br-` prefix, e.g. `make br-help` will show help output from the Buildroot Makefile, while `make help` will only show help from the Thingino Makefile.

### Building a Package 

Prefixed Buildroot `make` directives to work with a package at different stages:

- `br-[pkgname]`                         - Build and install [pkgname] and all its dependencies
- `br-[pkgname]-source`                  - Only download the source files for [pkgname]
- `br-[pkgname]-extract`                 - Extract [pkgname] sources
- `br-[pkgname]-patch`                   - Apply patches to [pkgname]
- `br-[pkgname]-depends`                 - Build [pkgname]'s dependencies
- `br-[pkgname]-configure`               - Build [pkgname] up to the configure step
- `br-[pkgname]-build`                   - Build [pkgname] up to the build step
- `br-[pkgname]-dirclean`                - Remove [pkgname] build directory
- `br-[pkgname]-reconfigure`             - Restart the build from the configure step
- `br-[pkgname]-rebuild`                 - Restart the build from the build step
- `br-[pkgname]-reinstall`               - Restart the build from the install step
- `br-[pkgname]-show-info`               - Generate info about [pkgname], as a JSON blurb
- `br-[pkgname]-show-depends`            - List packages on which [pkgname] depends
- `br-[pkgname]-show-rdepends`           - List packages which have [pkgname] as a dependency
- `br-[pkgname]-show-recursive-depends`  - Recursively list packages on which [pkgname] depends
- `br-[pkgname]-show-recursive-rdepends` - Recursively list packages which have [pkgname] as a dependency
- `br-[pkgname]-graph-depends`           - Generate a graph of [pkgname]'s dependencies
- `br-[pkgname]-graph-rdepends`          - Generate a graph of [pkgname]'s reverse dependencies
- `br-menuconfig`                        - Run Buildroot menuconfig
- `br-savedefconfig`                     - Save board defconfig
- `br-busybox-menuconfig`                - Run BusyBox menuconfig
- `br-linux-menuconfig`                  - Run Linux kernel menuconfig
- `br-linux-savedefconfig`               - Run Linux kernel savedefconfig
- `br-linux-update-defconfig`            - Save the Linux configuration to the path specified by BR2_LINUX_KERNEL_CUSTOM_CONFIG_FILE
- `br-list-defconfigs`                   - List all defconfigs (pre-configured minimal systems)
- `br-source`                            - Download all sources needed for offline-build
- `br-external-deps`                     - List external packages used
- `br-legal-info`                        - Generate info about license compliance
- `br-show-info`                         - Generate info about packages, as a JSON blurb
- `br-pkg-stats`                         - Generate info about packages as JSON and HTML
- `br-printvars`                         - Dump internal variables selected with VARS=...
- `br-make V=0|1`                        - 0 => quiet build (default), 1 => verbose build

Thingino adds a few shortcut directives of its own:

- `bootstrap`                            - Install prerequisites
- `clean`                                - Remove `target` directory and `.config` file for the given board
- `distclean`                            - Remove all building files for the given board
- `rebuild-[pkgname]`                    - Combine `dirclean` and `rebuild`
- `pack_full`                            - Download a corresponding bootloader and create a full firmware file
- `pack_update`                          - Create a firmware update file without a bootloader
- `update_ota IP=192.168.1.10`           - Upload and install firmware update, leave bootloader and most settings
- `upgrade_ota IP=192.168.1.10`          - Upload and install full firmware including bootloader

---

## Toolchains

### Available Toolchains for XBurst Development

These toolchains are designed to support various Ingenic SoC targets and leverage different versions of GCC (GNU Compiler Collection) and libc implementations (GNU and musl).

#### Toolchain Overview

The following toolchains are available for development:

- **GNU GCC Toolchains for XBurst1:**
  - `toolchain_xburst1_gnu_gcc12`
  - `toolchain_xburst1_gnu_gcc13`
  - `toolchain_xburst1_gnu_gcc14`
- **Musl GCC Toolchains for XBurst1:**
  - `toolchain_xburst1_musl_gcc12`
  - `toolchain_xburst1_musl_gcc13`
  - `toolchain_xburst1_musl_gcc14`
- **Musl GCC Toolchains for XBurst1 (Kernel 4.4):**
  - `toolchain_xburst1_musl_4_4_gcc13`
  - `toolchain_xburst1_musl_4_4_gcc14`

#### Target SoCs

- **XBurst1 Targets:**
  - T10/T20/T21/T23/T30/T31 SoCs
- **XBurst2 Targets:**
  - A1/T40/T41 SoCs

#### GCC Versions

The toolchains are based on multiple versions of the GCC compiler:

- GCC 12
- GCC 13
- GCC 14

These versions ensure compatibility with a wide range of software, offering developers the flexibility to choose a toolchain that best suits their project's requirements.

#### Choosing a Toolchain

When selecting a toolchain for your project, consider the following:

- **Target Architecture:** Ensure the toolchain supports your SoC (XBurst1 vs. XBurst2).
- **Libc Implementation:** Decide between GNU libc and musl libc based on your project's needs. Musl libc is designed for static linking and simplicity, while GNU libc offers extensive features and dynamic linking support.  
- `Musl is the default recommended toolchain for Thingino development.`
- **GCC Version:** Newer versions of GCC may offer better optimizations and more features. However, compatibility with your codebase should be verified.

#### Getting Started

Up to date Toolchains releases are always available on the [releases](https://github.com/themactep/thingino-firmware/releases/tag/toolchain) page.  Toolchains are updated weekly.

---

## Containers

### Overview
Are you interested in building or developing with Thingino but concerned about cluttering your system with additional software or needing to upgrade your operating system? Container technologies provide a streamlined solution to maintain a clean and efficient workspace. Whether you're building firmware or developing extensively, containers like Docker and LXC offer isolated environments tailored to your needs.

### Docker for Firmware Building
**Docker** provides a lightweight environment ideal for users focusing on firmware compilation without altering their system setup. It offers:
- A Debian-based container that ensures consistency across different systems.
- Minimal setup time with immediate readiness for firmware configuration.
- A simple interface to facilitate the build process.

### LXC for Comprehensive Development
For a more in-depth development experience, **LXC (Linux Containers)** offers a robust environment:
- Closer-to-metal operations that provide enhanced control over the workspace.
- Traditional VM-like behavior suitable for detailed testing and debugging.
- Provides an environment that can handle not only firmware compilation but also detailed testing and debugging.
- An ideal choice for developers requiring a full Debian system setup.

Both technologies ensure that your development does not interfere with your primary system, enhancing both security and efficiency.

### Quick Start Guides

#### Docker Setup
To start with Docker, clone the Docker environment repository and run the setup script:
```bash
git clone https://github.com/themactep/docker-worker.git ~/docker-worker
cd ~/docker-worker
./run.sh thingino
```

#### LXC Setup
LXC provides a Debian-like experience and is straightforward for users familiar with Debian systems. Here’s how to set it up:
```bash
git clone https://github.com/gtxaspec/thingino-lxc && cd thingino-lxc
sudo bash setup_thingino_lxc.sh
```
This script creates an LXC container named 'thingino-development', installs all necessary tools, and attaches you directly to the container for immediate development.

##### Accessing Your LXC Environment
To access your dedicated Thingino LXC environment:
1. Open your terminal.
2. Run `attach-thingino` to enter your development container.

**Exiting the Container:**
Type `exit` to return to your host system. Your container retains its state, allowing seamless continuation of your work.

##### LXC Installation Demo
For a visual guide, view our setup demonstration:

https://github.com/themactep/thingino-firmware/assets/12115272/f50f91c6-338b-4eaf-ac51-0a7e3248fb3b

### Benefits of Containerized Development
- **Isolation:** Keeps your main system pristine.
- **Reproducible:** Easy to replicate or remove environments without residual impacts.
- **Resource Efficiency:** Containers use fewer resources than full virtual machines, maintaining system performance.

Now, you're all set to enjoy hassle-free development with Thingino in a clean, organized environment!

[1]: https://buildroot.org/
[2]: https://buildroot.org/docs.html
[3]: https://github.com/buildroot/buildroot/compare/master...themactep:buildroot:master
[4]: https://github.com/themactep/thingino-firmware
