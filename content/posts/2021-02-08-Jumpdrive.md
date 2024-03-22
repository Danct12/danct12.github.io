---
date: "2021-02-08T00:00:00Z"
title: How I wrote Jumpdrive
categories:
- Software
tags:
- software
- pinephone
- pinetab
- pine64
- jumpdrive
- linux
---

**Image hasn't moved over yet, so there are currently no images in this post.**

A year ago, I have wrote Jumpdrive, a swiss army knife SD image for PinePhone and PineTab.

# The early days of PinePhone

Back in the early day of the PinePhone, in order to try out a new OS or a new image you'll need an SD card and flash the image using Etcher or dd. This is only temporary as once the SD card is removed from the device, the phone will only boot to whatever is on eMMC.

If the user thinks that they like the OS, they can flash it to eMMC.. but there's one problem:

In order to flash an OS to eMMC you either:
- Boot to an OS on SD card, grab the image and flash it to eMMC all of this inside the OS.
- Boot to [FEL](https://sunxi.org/FEL) and flash it using sunxi-fel tool, more complicated than above

# Development

It was a night, while developing on postmarketOS I realized that since USB can be used to expose a network interface.. it can be used to expose other stuffs as well, right?? So I did some read up and figured that ConfigFS can also do MTP as well as a USB mass storage device!

Because of that, I put up a simple test image using Busybox and some shell scripting. As for the script, I took bits from postmarketOS init_functions and then add mmcblk2 (eMMC) as a mass storage device.

After done, I tried test it and unfortunately it crashes right on first boot! I had to add symlink to busybox for some of the module as they won't initialize properly and it works!

I released it on [GitHub](https://github.com/dreemurrs-embedded/Jumpdrive/releases/tag/0.1) under the name "RescueSD", but unfortunately that name gives confusion as there's no reason to use a rescue image if your phone is still working.. right?

So a few days later, Martijn Braam made a pull request and cleaned up my scripts (as the script I put up is just a PoC), and give it a new splash screen (the one you're seeing now)

And the project also made it's way to Ubuntu Touch, where it is being used as recovery system and also to update the OS!

[Image credit to Lukas Erecinski, WARNING: TWITTER LINK](https://twitter.com/LukaszErecinsk1/status/1255980305044910081)

Despite the release of Jumpdrive, some OS still have issues booting from eMMC such example would be [SailfishOS port for PinePhone](https://github.com/dreemurrs-embedded/Jumpdrive/issues/8). These depends on the maintainer of the OS to support, which they was really nice to support it.

Nowadays I don't work on Jumpdrive anymore, and Martijn Braam is the new maintainer. But I'm happy that my small work have helped the community moving this far.

Day 2 of #100DaysToOffload.
