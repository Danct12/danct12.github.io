---
date: "2022-07-10T00:00:00Z"
title: How to run Hypnospace Outlaw on ARM
categories:
- Tutorials
- Gaming
tags:
- hypnospace outlaw
- hypnospace
- arm
- gaming
- howto
---

**Image hasn't moved over yet, so there are currently no images in this post.**

While I was watching Vinesauce Joel a few months ago, I came across this game called Hypnospace Outlaw, a game where you play as a internet police in the 90s.

The game itself is great and fun, had many hours of fun and finished the game too. However, what interested me is that the game files seems to resemble a web application, and sure enough, it uses nw.js. And being a web application (like Electron), it should run on other platform like ARM (Raspberry Pi, Pine64, ODROID, ..) too.

# Prerequisites
- A copy of Hypnospace Outlaw (can be bought on Steam or other platform)
- A powerful enough board (it should run fine on a RK3399, but it's slow)

For this tutorial, I'll be using a Pinebook Pro which has Rockchip RK3399 SoC.

# Setting up a Nw.js instance
In order to run the game, we must do some work as the nwjs binaries that came with the game are for x86 and is not compatible.

Luckily, there's already made ARMv7/ARMv8 nw.js binaries and it can be downloaded [here](https://github.com/LeonardLaszlo/nw.js-armv7-binaries/releases), grab the one for your specific architecture (ARM64 builds can be identified by looking at the file name).

Download it, or if you want you can compile it on your own which will take a very long time unless you have a build cluster.

Once downloaded, open the zip file and navigate to `usr/docker/dist`, you'll find `nwjs-chromium-ffmpeg-branding` and look for `nwjs-*-linux-arm.tar.gz` (for me, current version is: nwjs-v0.60.1-linux-arm.tar.gz) and extract the tarball to somewhere.

As for Chrome or Chromium branding, it doesn't matter. What Chrome branding build does is for proprietary codecs, HypnOS doesn't use that, so just stick to the Chromium build.

Now you need to copy `data` folder and `package.nw` from Hypnospace Outlaw's game directory to the newly extracted folder with nw.js binaries in it.

# Launch it!
Now you should be able to launch the game, just run the `./nw` binary and the game should launch. If the game runs slow then your SoC might not be powerful enough (you can disable autoplay music to reduce workload).

Unfortunately I cannot get it to work on my PinePhone A64 due to some unsupported GPU issue, I might look into it.

