---
date: "2019-12-22T00:00:00Z"
title: Debian x86 chroot on ARM (w/o Exagear)
categories:
- Software
- Tutorials
tags:
- howto
- debian
- x86
- chroot
- arm
- exagear
- ubuntu
- pinetab
- pine64
---

Just in case if you're not happy with the selection of arm64 programs, you'll probably want to tap into the x86 part by running them!

# How can you run x86 Linux processes on ARM?
By using QEMU, we can launch x86 Linux processes which then QEMU will translate the syscalls to your CPU on the fly. This also works on other architecture (e.g. PowerPC, RISC-V, MIPS,..) as long as QEMU is compiled for the platform.

# Requirements
- Target system
- root access
- Coffee/Tea or whatever drink **(optional)**

# Target system
All of this will be done on PineTab by Pine64, the following specs are:
- SoC: [Allwinner A64](https://linux-sunxi.org/A64)
- RAM: 1GB (DDR3) **the final unit will ship with 2GB of RAM**
- GPU: Mali-400MP2
- SD Card: 32 GB Toshiba UHS-1

# Prepare the system

## Kernel
Nothing much needs to be changed, just make sure `CONFIG_BINFMT_MISC` is compiled to kernel. 

On most kernels this should be enabled by default, but can be checked by `zcat /proc/config.gz | grep BINFMT_MISC`.

## Dependencies
Those packages are required:
- qemu-user-static
- schroot
- debootstrap

All those packages can be installed with one command:
- **Ubuntu/Debian**: `apt-get install qemu-user-static schroot debootstrap`
- **Arch Linux ARM**: `yay -S qemu-user-static schroot debootstrap`

For other distributions, please look for those packages by yourself.

# Setup a x86 chroot
Create a folder where you want to store the Debian x86 chroot, in this case I'd like it to be in `/srv/chroot/debian-x86`, so you need to run `mkdir -p /srv/chroot/debian-x86` (as root)

From now on `/srv/chroot/debian-x86` will be our target directory for Debian.

Now you'll have to look for a Debian mirror, I'll be using `http://debian.xtdv.net/debian` because it's the fastest mirror for me.

Next thing we're gonna do is to install Debian 9 (Stretch):
```console
# debootstrap --arch i386 --foreign stretch /srv/chroot/debian-x86 http://debian.xtdv.net/debian
```
- --arch: Set the target architecture, in this case it's i386, you can use x86_64 if you want.
- --foreign: Only run first stage bootstrap, second stage requires QEMU to be in the chroot installation.

A few moment later, you should be back to shell, now you need to copy `qemu-i386-static` to `/srv/chroot/debian-x86/usr/bin`
```console
# cp /usr/bin/qemu-i386-static /srv/chroot/debian-x86/usr/bin
```

We're now ready to run the second stage of debootstrap:
```console
# chroot "/srv/chroot/debian-x86" /debootstrap/debootstrap --second-stage
I: Installing core packages...
```
Sit back and relax, and maybe take a silp of coffee, dunno, because this will take **a while** depends on your eMMC/SD Card speed.

Later you'll get a message that the base system has successfully installed.

# Finishing x86 chroot setup
If you made it to here, you're almost done, keep going!

Create a new file `/etc/schroot/chroot.d/debianx86.conf`, this is where the schroot configuration will be.
```ini
[debian-x86]
description=Debian Stretch x86 chroot
aliases=debian-x86
type=directory
directory=/srv/chroot/debian-x86
profile=desktop
personality=linux
preserve-environment=true
```

Now you can chroot to the x86 system by using schroot, come on, it feels like home here.
```console
[alarm@alarm ~]$ sudo schroot -c debian-x86
W: line 3 [debian-x86] aliases: Alias ‘debian-x86’ already associated with ‘unknown’ chroot
(debian-x86)root@alarm:/home/alarm# 
```
It's safe to ignore that warning for now, but now you're inside the Debian x86 chroot!

We need to run `apt-get update` to update and obtain the key signatures as it hasn't setup yet and now you have finished setting up a Debian x86 chroot.

One thing to notice is that the /home directory is linked to the chroot, meaning that you can access your actual home directory from the chroot, this makes it easier to work with.

Keep in mind that users, groups and passwords configuration are copied every time you access schroot, this means that you can run executables under your current, non-root user without doing any additional setup, just `su` to the target user (in this case `alarm`).

X11 applications should work fine under the current user, too.

# Additional setup
It is recommend to comment out some files (e.g. passwd, shadow) in the nssdatabases if you don't want them to be overwritten:
`/etc/schroot/desktop/nssdatabases`

If you have any questions, feel free to comment down below.
