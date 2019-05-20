---
layout: post
title: Arch Linux on Xiaomi Redmi 4X
---

If you have followed me from the time when I did use my phone as a portable computer on the go, you might know that I have a weird fetish with phones, instead of doing phone things, you can just install X11 and run X11 applications.

Well, all of that stuff was done inside chroot and inside Android, so you're still using Android, just not in a Android UI. But then, why not start from the other side? Just boot to a Linux distribution instantly, no need to go through Android, Linux Deploy blah blah.

# Introducing (Arch) Linux on my phone, the Xiaomi Redmi 4X!
![Just Arch Linux.](https://raw.githubusercontent.com/Danct12/danct12.github.io/master/images/IMG_20190319_033954.jpg)

There it is, Arch Linux on Android phone, without chroot or VNC, running on Android kernel and [Arch Linux ARM] ramdisk, rootfs! No Android UI or Android environment, it's just Arch Linux ARM. And now I don't know what else to say here.

I was largely inspired by [postmarketOS], they booted the device to Alpine Linux without depending on Android, all you need was just the kernel source and the toolchain then you can build a port for it.

# How was this done?
Actually it wasn't that hard to be done, you can do it on other devices so it's not just Redmi 4X.

DanctNIX user @Asriel Dreemurr#8121 has made a guide on how to port Arch Linux to devices, which can be seen [here](https://github.com/Danct12/arch-linux-santoni/blob/master/Documentation/Porting_to_a_new_device.txt)

I've also made **PKGBUILD**s for Redmi 4X along for other devices as well, you can also find them on my repo:
[https://github.com/Danct12/arch-linux-santoni/tree/master/Arch_PKGBUILDs](https://github.com/Danct12/arch-linux-santoni/tree/master/Arch_PKGBUILDs)

# What it could do?
Pretty much anything that ARM devices can do, just with a few exceptions that it lacked driver supports due to the fact that the libs are compiled against and only for Android, but then for Wi-Fi and ADSP on Qualcomm devices that uses WCNSS, supplying the firmware files from /firmware inside Android to /lib/firmware/postmarketos in the rootfs could let the Wi-Fi driver be enabled on non-Androids.

I was able to start Xorg and XFCE4 on this device, however one problem is that the entire screen is rendered using fbdev, which is very slow and this will be even more slower on devices that has high resolution (2K, 4K,..), and even on high-end CPUs it's still slow.

Another problem is that fbcon driver is broken on Qualcomm devices, turning it on will not do anything, I've read that modprobing the fbcon driver after rootfs loaded is a workaround, through this doesn't work on MSM8937, it'll crash and becomes unusable until the device is hard rebooted.

Though, programs like Chromium supports multi-touch and can do gestures just fine.

# Can you make calls on it?
Nope, you can't call 911 or text someone. The modem isn't enabled, sadly.
I've tried to enable the modem, however it'll just not work and crash the modem instead.

# libhybris?
[libhybris] is my high priority, it enables the drivers and uses Android libs, which means that sensors, Bluetooth, and even HW acceleration will work! Through nothing has done yet as for current state.

I'll be looking into this, if there's anything being done, I'll make a followup blog post.

# Ending note
As and always, this will always void your warranty so be warned. It also will disconnect you and your phone from Android.

I'll also recommend you check out [postmarketOS], they did a very good job on this and Nexus 5, Z2 Tablet, Nokia N900 are the ready to use devices if you want to [dogfooding](https://en.wikipedia.org/wiki/Eating_your_own_dog_food) one of these device as a Linux system.

[Arch Linux ARM]: https://archlinuxarm.org
[postmarketOS]: https://postmarketos.org
[libhybris]: https://github.com/libhybris/libhybris
