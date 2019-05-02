---
layout: post
title: Exploring my home router - FPT
---

Just got a brand new router a few days ago, it was a switch from FPT after my old one got broke.
To be honest, I still like the old design, but the new design is okay, however it looks like the tower from OneShot.

In case if people didn't know, the old router firmware has a exploit in the diagnose section, you can do arbitrary code execution, as they did not escape commands, this time they did, but also they don't have anything to hide as this one have ssh/telnet access.

With that being said, let's dig right into it.

**DO THIS AT YOUR OWN RISK, I'LL NOT TAKE RESPONSIBLE FOR BRICKS, EXPLOSIONS OR THERMONUCLEAR**

Before exploring the wanderful world of this router, we'll need to enable SSH by going to the router control panel, head to Security Setup options and SSH.

![Router Control Panel]({{ site.baseurl }}/images/FPTRouter/sshcp.png)

**Please DO NOT enable remote SSH, this way, you can open a door for attackers to hijack your router, this might also compromise all systems connected to the router.**
Now you're ready to ssh to the system by ssh to the router gateway address.

When I SSH to the router, the screen cleared for some reason, probably not a fan of messy consoles. But that's not important, one thing is that it took me a bit while to find how to work with the router remote access, and I want a shell, a bit digging and here we are.

![Router Control Panel]({{ site.baseurl }}/images/FPTRouter/sshshell.png)

The CPU in this thing is RTL8672 SoC, it's architecture is MIPS, which is common on routers, but after a while digging around, the Huawei HG532C looks almost the same as my router, so probably it's just a rebranded router (with optical fiber)

This thing has Busybox v1.18.4, built in 2013, so they should try to upgrade Busybox in the next update.

The Busybox applets on the router is fairly limited *(not fairly but extremely)* to the point that I don't even know who I am!

![Router Control Panel]({{ site.baseurl }}/images/FPTRouter/lackcommands.png)

**mtd of this router:**
```
#ONT/system/shell>cat /proc/mtd
dev:    size   erasesize  name
mtd0: 000c0000 00020000 "Boot1"
mtd1: 00200000 00020000 "Config1"
mtd2: 01c00000 00020000 "ImageA"
mtd3: 01c00000 00020000 "ImageB"
mtd4: 00400000 00020000 "MidWare"
mtd5: 000c0000 00020000 "Boot2"
mtd6: 00200000 00020000 "Config2"
mtd7: 00e00000 00020000 "Imagec1"
mtd8: 00e00000 00020000 "Imagec2"
mtd9: 00100000 00020000 "eeprom1"
mtd10: 00100000 00020000 "eeprom2"
mtd11: 02000000 00020000 "OsgiA"
```

Unfortunately I was not able to download a copy of mtdblock root partition, even if I'm root for sure, I cannot get it to download, any attempt doing it will end up with Permission Denied.
