---
date: "2021-04-20T00:00:00Z"
title: VNC on PinePhone (how to)
categories:
- Tutorials
tags:
- pinephone
- vnc
- linux
- wlroots
- wayvnc
- howto
---

**Image hasn't moved over yet, so there are currently no images in this post.**

Having to pick up your phone every time when testing your application is very annoying, so having remote access is really convenient especially when I do development without the phone around.

**Keep in mind that I'm talking about Phosh and other wlroots-based environment. If your UI is not based on those (e.g. KWin), the instructions might be different.**

# Let's do it!

Before we get started, make sure that you need to have access to the phone (physically, or remotely via SSH). Got access to the device? Great.

Open up a Terminal (or SSH into the device) and install `wayvnc`, on Arch Linux ARM / Manjaro, you can install this package by typing:
```
$ sudo pacman -Sy wayvnc
```

Once that's done, you can now run wayvnc by running:

```
$ wayvnc [address] [port]
```

Remember to replace [address] [port] with:
- [address] : the local IP of your phone's network interface (alternatively use 0.0.0.0 to listen on all interfaces)
- [port] : the port that you want the vnc server to listen on, I choose 1703.

You may also want to check out manpage of wayvnc for additional parameters that may interest you.

After you run the command, it doesn't output anything to the terminal but the server has already started. You can use your favorite VNC client like KRDC or TigerVNC and connect to your phone using the IP and port you specified earlier.

Heck, it even works nicely over SSH tunnel. So even if you don't have access to your device, you can develop on the phone just like at home.

Day 4 of #100DaysToOffload.
