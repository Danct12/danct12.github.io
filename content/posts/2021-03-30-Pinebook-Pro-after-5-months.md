---
date: "2021-03-30T00:00:00Z"
title: Pinebook Pro as a daily driver (after 5 months)
categories:
- Hardwares
tags:
- laptop
- hardwares
- linux
- pinebook pro
- kde
- manjaro
- rockchip
---

**Image hasn't moved over yet, so there are currently no images in this post.**

I received the Pinebook Pro from PINE64 in November 2020, this is a cheap ARM64 laptop sold for 200$ (now 220$ due to chip shortages). The laptop specifications can be seen [here](https://www.pine64.org/pinebook-pro/).

# What do you do on the laptop?

I use this laptop for:
- Doing general things such as web browsing, chit chatting on Discord
- SSH access to my desktop computer for development
- Writing this article
- Playing games - SuperTuxKart, SuperTux2, **DOOM!!**
- Anything else that's possible

**I do not use this laptop at home** as my main desktop is what I use, but when I'm outdoors, this is the perfect laptop for me. Sure, the specs on surface doesn't look that really impressive, but it does get the job done for me.

# What OS do you use?
The OS I'm currently using on this laptop is Manjaro ARM, while I'm not a huge fan of Manjaro (btw i use arch), I have to appreciate the work that the team has done on the ARM platform.

I generally avoid using the prebuilt Manjaro + DE/WM image as I deemed it to be bloat for me, so I grabbed the minimal image for the Pinebook Pro and flashed it to the eMMC, this image only comes with the terminal and you can build your own environment on top of it.

Most of the 2D-only WM/DE runs poorly on the Pinebook Pro due to a bug in Rockchip DRM driver (I tried FVWM, WindowMaker) so until that's fixed, KDE Plasma is what I choose to be the final to-go desktop environment.

# The Good

One thing I like about this laptop is that the keyboard is nice to use, it doesn't have the best typing feels, but that is to be expected for this price.

The laptop could be charged either by the barrel jack, or USB-C. So if you don't have the barrel charger with you, you can charge the laptop using the USB-C port.

The killswitches are toggled by pressing Pine (aka Super) + F10-F12:

- F10: Microphone
- F11: Wi-Fi/BT
- F12: Camera

Those killswitches aren't software, rather it's the hardware cutting power to the components. This means, you will no longer need to tape your camera or microphone, but also helps save battery power as well.

Web browsing is great, although heavy websites struggles, but that's to be expected with the modern web.

When I'm bored from doing all of the works, playing games is the next thing to do! I usually play Classic Doom on it (using LZDoom port), it runs very great, same goes for SuperTux.

However SuperTuxKart is a bit laggy as it drops a lot frames when things getting intense, the forest map is the worst one. I had to rebind the key for kart skidding due to the keyboard matrix.

# The Bad (or not so great)
I do not like the trackpad, sometimes it can be jumpy. But you can plug in a mouse and disable the touchpad (Fn + F7) as it does have a killswitch for that on the keyboard so it's not really a big deal.

Video decoding are mostly done on GPU or CPU, there is currently a driver for video acceleration, but no libva yet although there is a driver for it, it's still a WIP and I couldn't get it to work. :(

Sleep states currently are broken, so putting it to sleep will make discharge your battery heavily. I hope to see that's fixed in the future, as it is very annoying.

# Conclusion
Now with that being said..

**Should you buy the Pinebook Pro?**

I would say it depends on your use case, if you do things like word processing, spreadsheets, web browsing or light development or you just want a cheap ARM64 laptop then this laptop is for you.

If you're looking for a high performance laptop to run Linux on so you could do stuffs like 3D rendering, gaming, you will have to spend more than that or you can buy a used laptop and install Linux on it.

Day 3 of #100DaysToOffload.
