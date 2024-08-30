> [!WARNING]
> WORK IN PROGRESS
> USE AT YOUR OWN RISK

### Booting U-Boot from NFS: A Step-by-Step Guide

This guide provides instructions on how to boot a device using U-Boot over NFS. The examples include booting with just a root filesystem (rootfs) and booting with both the rootfs and the kernel loaded over NFS.

### Prerequisites
1. **NFS Server Configuration**: Ensure your NFS server is configured to export the rootfs directory and is accessible from your device. 
3. **Network Configuration**: Configure your network settings (IP, gateway, server IP) correctly.

### NFS Server Setup

On the server, you need to export the rootfs directory:

```bash
/mnt/exported/path *(rw,no_root_squash,no_subtree_check,sync)
```

Make sure the NFS server is running and properly configured to allow connections from the client device.

### U-Boot Configuration

#### 1. **Set Up U-Boot Environment Variables**

Start by setting the necessary environment variables:

```bash
setenv enable_updates true
setenv ipaddr 192.168.1.100       # IP address of the device
setenv gatewayip 192.168.1.1      # Gateway IP
setenv serverip 192.168.1.10      # IP address of the NFS server
setenv nfsroot /mnt/exported/path # NFS server export path
```

#### 2. **Booting with NFS Root Filesystem**

To boot using only the root filesystem over NFS, set the following `bootargs`:

```bash
setenv bootargs 'mem=${osmem} rmem=${rmem} console=${serialport},${baudrate}n8 panic=${panic_timeout} init=/init root=/dev/nfs rootfstype=nfs ip=dhcp nfsroot=${serverip}:${nfsroot},v3,nolock rw mtdparts=jz_sfc:256k(boot),64k(env),${kern_size}(kernel),${rootfs_size}(rootfs),-(rootfs_data)${update}'
boot
```

#### 3. **Loading Kernel from NFS**

To load the kernel image from NFS and then boot, use the following commands:

```bash
setenv kernel_image /mnt/exported/path/uImage
setenv loadaddr ${baseaddr};
nfs ${loadaddr} ${serverip}:${kernel_image}
bootm ${baseaddr};
```

This sequence sets the kernel image path and loads it from the NFS server into memory, followed by booting the kernel.

#### 4. **Loading Both Kernel and Root Filesystem from NFS**

For loading both the kernel and root filesystem from NFS, the steps are as follows:

```bash
setenv enable_updates true
setenv ipaddr 192.168.1.100
setenv gatewayip 192.168.1.1
setenv serverip 192.168.1.10
setenv nfsroot /mnt/exported/path
setenv kernel_image /mnt/exported/path/uImage

setenv bootargs 'mem=${osmem} rmem=${rmem} console=${serialport},${baudrate}n8 panic=${panic_timeout} init=/init root=/dev/nfs rootfstype=nfs ip=dhcp nfsroot=${serverip}:${nfsroot},v3,nolock rw mtdparts=jz_sfc:256k(boot),64k(env)'

setenv bootcmd 'setenv loadaddr ${baseaddr};nfs ${loadaddr} ${serverip}:${kernel_image};setenv setargs setenv bootargs ${bootargs};run setargs;bootm ${baseaddr};'

boot
```
This setup ensures both the kernel and the root filesystem are loaded over NFS.

### Saving Configuration

To retain the setup across reboots, save the environment variables by running `saveenv`.

### Troubleshooting

- **NFS Version Support**: Thingino's U-Boot supports NFS v2 or v3. Ensure that your server is configured to support one of these versions.  
- **UDP Support**: U-Boot in this setup requires UDP for loading the kernel via NFS, so ensure your NFS server is configured to allow UDP for this purpose. For loading the root filesystem, UDP is not required. Alternatively, you can use TFTP to load the kernel instead of NFS.  

### Notes

- Replace the IP addresses and paths with your actual network configuration and server paths.
- For documentation purposes, the IP ranges and paths used are within the private range specified for examples.

This guide should help you boot your device for rapid development using U-Boot over NFS, whether you're loading just the rootfs or both the rootfs and kernel.