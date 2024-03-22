---
date: "2019-08-29T00:00:00Z"
title: Arch Linux ARM on Pine64's PineTab
categories:
- Software
- Tutorials
tags:
- pinetab
- arch linux arm
- linux
- howto
---

Few weeks ago, I received a package from Pine64, yes, that Pine64 which makes single board computers and the most important, the upcoming PinePhone!

I've been working on the PineTab and postmarketOS for a few weeks now, but today I wanted to try out something new, so let's run Arch Linux ARM on my PineTab.

## Getting started
To do this, I used my trusty compiling dummy (which is also my main computer), my PineTab I received for development and of course, you need to have a **SOUL** and **DETERMINATION**.

### Compiling kernel
To compile kernel, you need a cross-compiler toolchain, luckily if you're using Arch Linux, it's also packaged and can be installed by `pacman -S aarch64-linux-gnu-gcc`

Since drivers (display panel, device tree,...) aren't upstreamed to [mainline Torvalds tree](https://github.com/torvalds/linux) yet, we'll have to use the [kernel tree from Pine64](https://gitlab.com/pine64-org/linux).

You can make up your own PKGBUILD for this, however if you don't want to make one, you can use mine which I've modified from `linux-aarch64` package from ALARM and the PKGBUILD for kernel, also other PKGBUILDS can be found [here](https://github.com/Danct12/Pine64-Arch/tree/master/PKGBUILDS).

You can't makepkg yet, because your system is set to x86_64.

To get around this, I made my own custom makepkg-aarch64-kernel.conf just to compile this kernel, and which this will probably not gonna work on other packages as it may link your native binaries and those won't run on your PineTab.

The only changes to the makepkg.conf is following:
```
CARCH=arm64
```

Make sure this is a custom makepkg config file, since the default config file is for compiling native packages on your native system.

Once that's done, make sure you change the PKGBUILD variables for `CROSS_COMPILE` to `aarch64-linux-gnu-` and `ARCH` to `arm64`. And now start compile using `makepkg --config *path to your custom makepkg config* -s`, then you should have a compiled kernel after you waiting. :)

## Install Arch Linux to SD Card

### Partitioning
Allwinner SoCs can boot a operating system through eMMC, or SD Cards, which is something I like from Allwinner systems. So for this, I use my 32 GB SD Card from Toshiba.

Plug in the card, and now you need to make a partition for rootfs (and optionally another partition for swap). And format the rootfs as ext4, which is very commonly used.

The end result for the partition layout should be like this:
```
Disk /dev/sdc: 29.54 GiB, 31708938240 bytes, 61931520 sectors
Disk model: Mass-Storage    
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x6996aa25

Device     Boot    Start      End  Sectors  Size Id Type
/dev/sdc1           2048 58011647 58009600 27.7G 83 Linux
/dev/sdc2       58011648 61931519  3919872  1.9G 82 Linux swap / Solaris
```

After that, you can mount the rootfs partition and extract Arch Linux ARM rootfs to it.

### Extract the rootfs
Mount the rootfs partition you just formated to somewhere (for this I use /mnt).

Now you need to download the ALARM rootfs [here](http://os.archlinuxarm.org/os/ArchLinuxARM-aarch64-latest.tar.gz), then run `bsdtar -xpf ArchLinuxARM-aarch64-latest.tar.gz -C mountpoint` as root (replace mountpoint as where you mounted your rootfs, which for me, I use /mnt)

### Access the aarch64 chroot on x86_64
You'll need a static binary of `qemu-aarch64-static` which can be downloaded from [here](https://github.com/multiarch/qemu-user-static/releases/tag/v4.0.0-4) (or compile it on your own if you want).

Once you got it, copy it to `mountpoint/usr/bin`. Now you can use arch-chroot script (from `arch-install-scripts`) to access the aarch64 chroot (or you can manually mount it and chroot)

### Let's configure the rootfs!

**Before you do this, `pacman -Syu` the chroot first!**

#### Install the kernel
**First thing first, uninstall the `linux-aarch64` package first, otherwise mkinitcpio will generate a initramfs that doesn't match your kernel!**

Once you done that, copy the compiled pkg file for the kernel, which should be in the directory you ran makepkg on and ends with *.pkg.tar.gz. Optionally, you can also get the kernel headers and install them if you're planning to compile kernel modules on the PineTab very later.

The kernel packages can be installed by running `pacman -U *.pkg.tar.gz`.

#### Generate U-Boot script
Now with the kernel packages installed, now you'll need to install `uboot-tools` to generate a U-Boot boot script.

Create a boot.txt file and put it in somewhere that you can access later (in case if you want to make changes to the boot parameter, I put it in /boot) with this contexts:

```
# Set root partition to the second partition of boot device
part uuid ${devtype} ${devnum}:${bootpart} uuid

setenv bootargs console=${console} console=tty0 fbcon=rotate:1 root=PARTUUID=${uuid} rw rootwait

if load ${devtype} ${devnum}:${bootpart} ${kernel_addr_r} /boot/Image; then
  setenv fdtfile allwinner/sun50i-a64-pinetab.dtb
  if load ${devtype} ${devnum}:${bootpart} ${fdt_addr_r} /boot/dtbs/${fdtfile}; then
    if load ${devtype} ${devnum}:${bootpart} ${ramdisk_addr_r} /boot/initramfs-linux.img; then
      booti ${kernel_addr_r} ${ramdisk_addr_r}:${filesize} ${fdt_addr_r};
    else
      booti ${kernel_addr_r} - ${fdt_addr_r};
    fi;
  fi;
fi
```

This command will generate the U-Boot script:
`mkimage -A arm -O linux -T script -C none -n "U-Boot boot script" -d boot.txt /boot/boot.scr`

Then configure the rootfs to sastify your needs.

If you want to compile packages, make sure get `base-devel` as well.

And now you're done, unmount the rootfs and let's install U-Boot!

## Install U-Boot
Since I haven't figured out how to compile U-Boot PKGBUILD yet, I'll use the U-Boot from Alpine Linux and you can also get that [here](https://github.com/Danct12/Pine64-Arch/blob/master/U-Boot/u-boot-sunxi-with-spl.bin)

`dd if=u-boot-sunxi-with-spl.bin of=/dev/sdcard bs=8k seek=1`

**Remember the replace /dev/sdcard with the actual SD Card device!**

## Let's boot
After you're done... make sure you unmounted the SD Card, make sure there's no more changes being written (best is to eject it from Linux first, then you can remove it physically.

Pop the card to your PineTab, and boot it up.

You noticed is that the screen stayed black and booted straight to Arch, this is because that U-Boot doesn't have support for DSI yet, meaning that there won't be any splash screen.

One thing to check to make sure that if it's working or not, Pine64 also supply you the serial cable if you got the PineTab prototype unit, so plug it in to your PineTab, and pop to the serial ttyUSB0 (115200n8) to have the U-Boot shell!

## Ending Note
Your PineTab is now running Arch Linux, congrats! However if you have configured the rootfs to have support for Wi-Fi, then you should be able to connect to the internet.

If you want to cross-compile ARM packages, you should try to use distcc!

PKGBUILDS for other stuffs can be found here as well: https://github.com/Danct12/Pine64-Arch
