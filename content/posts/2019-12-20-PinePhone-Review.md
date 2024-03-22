---
date: "2019-12-20T00:00:00Z"
title: PinePhone Review
categories:
- Hardwares
tags:
- hardwares
- phone
- linux
- pinephone
- pine64
---

**Image hasn't moved over yet, so there are currently no images in this post.**

A week ago, I received PinePhone Developer Edition (braveheart isn't out the factory yet), the device is put in bubble wrap, and placed inside a plastic box. Along with the phone, I also received another Pine64 UART cable and a USB-C Hub.

# Hardware
The hub has Ethernet, two USB ports (one of them is SuperSpeed) and a full-size HDMI port.

The PinePhone itself looks pretty good, 5.9 inch display with resolution of 720x1440, and it's larger than my current daily driver (Xiaomi Redmi 4X). It has RGB LED, a front-facing camera, and on the back, there is a rear camera, flash/lamp.

The back cover is replaceable as it can be removed, exposing a custom Samsung Galaxy J7 form-factor battery, which is very nice to see phones with removable battery, something that many phone manufacturers blindly took away.

On the top right corner, there are six killswitches, this can be used to cut the power to certain components:
1. **Modem:** On enables 2G/3G/4G communication and GNSS hardware, off disables.
2. **WiFi/BT:** On enables Wi-Fi and Bluetooth communication hardware, off disables.
3. **Microphone:** On enables audio input from on-board microphones (not 3.5mm jack), off disables.
4. **Rear camera:** On enables the rear camera, off disables.
5. **Front camera:** On enables the front camera, off disables.
6. **Headphone:** On enables audio input and output via the 3.5mm audio jack, off switches the jack to hardware UART mode.

These yellow pads are I2Cs, these are used by hardware manufacturers to create custom accessories for the PinePhone, which as of right now.. I don't see any, but if there are someone currently making one, I'd love to see keyboard accessory for it, as it is a phone for Linux users and.. probably hacking.

See that shiny piece of metal at the left corner? That's the [Quectel EG25-G] modem, this chip is responsible for 2G/3G/4G communication, as well as GNSS.

On the side, there is volume rocker and power button, it's the exact same thing on the PineTab. And one of my favorite feature from the phone that it includes a headphone jack, this is something that some phones are getting taken away, and it's also responsible for UART as well.

At the bottom, there is USB-C™, this phone supports Quick Charge (5V - 3A) unlike my Redmi 4X, OTG and DisplayPort.

# Software
The eMMC in this phone is 16 GB, and contain a factory test image of Android Nougat despite TL said it won't, but that's not a big deal. However the factory test image doesn't support touch screen.

So how do you install a properly working OS? Well, Allwinner SoCs supports booting from SD Card, so you can flash a Linux distribution to the SD Card, insert the SD Card to the device, then boot the device, it should boot straight away to the SD Card.

My flavour is [postmarketOS], so I installed it to the SD card using pmbootstrap rather than getting a dd-ready image off the site. For the choice of UI, I use [Plasma Mobile].

The front camera isn't working yet, however there is some WIP progress done on the camera. USB OTG used to work, but from what I heard there is a display bridge chip and that causes OTG to stops working, however that could be fixed by getting the driver for the chip to work.

The phone graphics is powered by Mali400-MP2, which uses the Lima FOSS driver, supports GLESv2. I haven't done any benchmark on the CPU yet, but from my testing, the UI seems to runs pretty smooth.

As for the modem, my unit came in with a defective modem which makes the device shuts off or not working properly, had to killswitch it so I don't have a chance to test it but UBports managed to make calls, and SMS also works too.

Currently, the kernel is custom and heavily patched, but thankfully they're trying to make it's way to upstream Linux, several patches have been posted to LKML.

# Conclusion
Regular smartphones are all riddled with vendor kernels which they're unwilling to upstream their changes, and I was wondering when can someone can make a phone with it's components compatible with upstream Linux drivers, but seems like the dream has come true.

I'm very sastified about this phone, this can be my daily driver only if the modem hasn't [DoA]. But seeing the work being done by the community, the phone might be usable before March 2020.

You should also check out [Drew Devault's Review](https://drewdevault.com/2019/12/18/PinePhone-review.html) on the PinePhone.

[Quectel EG25-G]: https://www.quectel.com/product/eg25g.htm
[Plasma Mobile]: https://www.plasma-mobile.org
[DoA]: https://en.wikipedia.org/wiki/Dead_on_arrival
[postmarketOS]: https://postmarketos.org

