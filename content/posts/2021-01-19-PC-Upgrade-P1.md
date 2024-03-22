---
date: "2021-01-19T00:00:00Z"
title: Make my desktop computer better - Pt 1
categories:
- Hardwares
tags:
- hardware
- desktop
- computer
- upgrade
---

Hey readers!

I've been my own self-built computer for a while now (i7-6700k, 8GB RAM and 1050 Ti) and everything has been great so far for years now.

But for a while now my computer has been slowing to a crawl, booting Arch Linux took around a minute to pass through the scrolling lines of text, and then a few minutes to start KDE desktop. Programs starts very slow on first boot, but it becomes faster as disk cache goes. So I decided to upgrade my computer. I've planned on a new hard drive (4TB), an SSD (500GB) and more RAM as I don't want to go swapping

# Parts that I need

However here's my goal:
- It should be around my budget (somewhere around 200$)
- Avoid no-name or "I haven't heard before" brands
- No second hand parts, you will never know if they fail in the future without any warranty.

**Now, I do not mean that you should not get things second hand, I prefer to get first hand on my stuffs, but to each of their own.**

For SSD I went with a Crucial P2 500GB, this is a M.2 drive and can be installed directly to the motherboard without additional wiring. It's gonna be mostly for rootfs, /home and Windows 10 LTSC.

For HDD, I had a hard time choosing either Seagate or Western Digital, they both are reputable brands I know, but I had a 1TB Seagate Barracuda failed on me (stuck head) and I heard other horror stories about Seagate drives. However someone from my community reported that their Seagate drive works perfectly fine for years and it has never failed. But I decided not taking any chances and went with WD Blue 4TB.

Fun fact, two of my other drives I have are from WD (green), and they still work perfectly fine after 10 years!

The last thing is RAM, I had a hard time looking for the same 8 GB stick, and even if I found one they aren't cheap, so I settled on a 16GB stick of Corsair Vengeance LPX DDR4. (24GB \o/)

I ordered them and this reseller apparently was really nice, they arrived the next day after I placed a call.

# Upgrade time!

Now onto the upgrade..

I should mention that you should:
- Unplug the computer from main power and press power button, this discharges the remaining power from the system.
- If you're standing on a carpet or wearing shoes, I suggest get anti static bracelet ([cordless straps are fake](https://www.youtube.com/watch?v=4-rO70_h0ck))
- Be careful around your equipment

For RAM upgrade, this was pretty easy, just put it in and push until it click.

Installing the HDD requires a SATA cable which they also included as a gift, I started taking out the tray and put the drive in and secure it with screws. And connect the drive to SATA power and data.

When I go and install my M.2 SSD, disaster struck.

I realized that I somehow lost the M.2 stand/screw that came with my motherboard, I do not know how long, but that was disappointing. I tried go out and look to see if anyone sell them but apparently they don't so pretty much I had to look on the internet again, I should have done that before starting the upgrade but oh well.

I bought it, but in order to get free shipping I had to buy a bit more so I also bought PCI covers too. Few days later they arrived, but it seems like that the price I bought was two set of them, so 1 = 2, 2 = 4 and so on, same goes for the PCI covers.

In order to install the M.2 stand, you need to locate how locate the screw hole for your SSD size, mine is 2280 so I tighten the screw mount to there. And then SSD, screw and done!

# What to do next

Upon boot up, the BIOS setup recognized by new HDD, as well as the 24GB RAM, but the SSD is nowhere to be seen in the BIOS. Booting to Linux shows the M.2 as /dev/nvme0n1p1.

Now to initialize my 4TB HDD.. I'll be using BTRFS as you can take a snapshot of your drive so when you deleted a file, you can undelete it by looking at the snapshot if you have saved it.

I'll do a write up on transferring my current installation to the SSD, but for now this is where it ends.

Day 1 of #100DaysToOffload
