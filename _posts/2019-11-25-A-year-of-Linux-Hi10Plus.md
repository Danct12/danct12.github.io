---
layout: post
title: A year of using Linux on Chuwi Hi10 Plus tablet
---

![]({{ site.baseurl }}/images/ChuwiHi10/IMG_20191125_105804-blurred.jpg)

<style>
table, th, td {
  border: 2px solid black;
}

th, td {
  padding: 4px;
}
</style>

Oh boy, it's been (almost) a year since my last post on how my x86 tablet performs in daily use. If you haven't seen it yet, [go and look at it if you want to]({{ site.baseurl }}/Three-Months-Hi10P/). =)

The tablet specs can be seen here: [https://www.chuwi.com/product/items/Chuwi-Hi10-Plus.html](https://www.chuwi.com/product/items/Chuwi-Hi10-Plus.html)

# Just use Windows 10, you're supposed to use it
## [No.](https://www.privacytools.io/operating-systems/#win10)
Other than that, there are plenty reasons why all I want is just GNU/Linux.

# Drivers Support?
It's nearly finished as far I can tell, some of them requires **proprietary blobs**.

Here is "what's working/not-working" list:

<table border="1">
  <thead>
    <tr>
      <th>Components</th>
      <th>Status (5.3.12)</th>
      <th>Requires Blob?</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Internal MMC</td>
      <td style="text-align: center; background-color: #cfffbf">Yes</td>
      <td></td>
    </tr>
    <tr>
      <td>SD Card Slot</td>
      <td style="text-align: center; background-color: #ffcfa5">Partial</td>
      <td></td>
    </tr>
    <tr>
      <td>GPU</td>
      <td style="text-align: center; background-color: #cfffbf">Yes</td>
      <td></td>
    </tr>
    <tr>
      <td>MicroUSB Port</td>
      <td style="text-align: center; background-color: #cfffbf">Yes</td>
      <td></td>
    </tr>
    <tr>
      <td>Type-C® Port</td>
      <td style="text-align: center; background-color: #cfffbf">Yes</td>
      <td></td>
    </tr>
    <tr>
      <td>USB Hubs</td>
      <td style="text-align: center; background-color: #cfffbf">Yes</td>
      <td></td>
    </tr>
    <tr>
      <td>Touchscreen</td>
      <td style="text-align: center; background-color: #cfffbf">Yes</td>
      <td style="text-align: center; background-color: #a55858">Yes</td>
    </tr>
    <tr>
      <td>Keyboard/Touchpad Case</td>
      <td style="text-align: center">???</td>
      <td></td>
    </tr>
    <tr>
      <td>WLAN (RTL8723BS)</td>
      <td style="text-align: center; background-color: #cfffbf">Yes</td>
      <td style="text-align: center; background-color: #a55858">Yes</td>
    </tr>
    <tr>
      <td>Bluetooth (RTL8723BS)</td>
      <td style="text-align: center; background-color: #cfffbf">Yes</td>
      <td style="text-align: center; background-color: #a55858">Yes</td>
    </tr>
    <tr>
      <td>Sounds (Speakers + Headphones)</td>
      <td style="text-align: center; background-color: #cfffbf">Yes</td>
      <td style="text-align: center; background-color: #a55858">Yes</td>
    </tr>
    <tr>
      <td>Microphone</td>
      <td style="text-align: center; background-color: #cfffbf">Yes</td>
      <td style="text-align: center; background-color: #a55858">Yes</td>
    </tr>
    <tr>
      <td>HDMI Output</td>
      <td style="text-align: center; background-color: #cfffbf">Yes</td>
      <td></td>
    </tr>
    <tr>
      <td>HDMI Audio</td>
      <td style="text-align: center; background-color: #cfffbf">Yes</td>
      <td></td>
    </tr>
    <tr>
      <td>Battery/Charging</td>
      <td style="text-align: center; background-color: #cfffbf">Yes</td>
      <td></td>
    </tr>
    <tr>
      <td>Backlight</td>
      <td style="text-align: center; background-color: #cfffbf">Yes</td>
      <td></td>
    </tr>
    <tr>
      <td>Hardware Buttons</td>
      <td style="text-align: center; background-color: #cfffbf">Yes</td>
      <td></td>
    </tr>
    <tr>
      <td>Light Sensor (CM3218)</td>
      <td style="text-align: center; background-color: #a55858">No</td>
      <td></td>
    </tr>
    <tr>
      <td>Accelerometer (BMA250)</td>
      <td style="text-align: center; background-color: #a55858">No</td>
      <td></td>
    </tr>
    <tr>
      <td>Camera</td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <td>Stylus Pen</td>
      <td style="text-align: center">???</td>
      <td></td>
    </tr>
  </tbody>
</table>

# My setup
For this, I use [Arch Linux], which is a rolling release distro, so the results can be what you're expecting to be on a kernel.org release.

On October of this year, I reinstalled Arch Linux because it was quite bloated with my own configuration, things such as USB standby and a bunch more, so I decided to start fresh.

After I reinstalled Arch, I installed XFCE since I decided to go with a floating type desktop, I could setup floating on i3, but that destroyed the purpose of having a tiling WM.

For the theme, I just don't want to rice it much, so I use Equilux for the theme, and the default WM theme.

![]({{ site.baseurl }}/images/ChuwiHi10/Screenshot_2019-11-26_09-11-24.png)

# Browsing
For this, I'm using Chromium 78.0.3904.97 (maximbaz build).

As far I can tell, web browsing experience on this tablet is fine for most parts, however intense HTML5 websites may suffer, but that's because websites have gone through so many changes, so better avoid them if you don't want to bake your Z8350. :)

But for most parts, I do review merge requests and issues for postmarketOS, which uses GitLab and going through random GitHub repository seems to be fine as it is designed for such computers.

As for [Twitter](https://twitter.com/RealDanct12) and [Mastodon](https://fosstodon.org/@danct12), it may be a bit too much but the experience is alright.

I don't recommend [YouTube](https://youtube.com/danct12cp) since it eats your CPU usage... quite alot.

# Video Decoding
Intel CPUs uses VA-API to decode media files and the Z8350 seems to decode H264, HEVC, MPEG2 and VP8 just fine, you just need to install [libva-intel-driver] then you can watch your favorite movies with HW decoding.

Alternatively, you can use [Big Buck Bunny] to test video decoding as it's a free movie.

## Video Decoding for Browser
Chromium (from Official Arch Linux repository) is not compiled with support for VAAPI, so you'll have to get [chromium-vaapi]ᵃᵘʳ or [chromium-vaapi-bin]ᵃᵘʳ.

Make sure you have installed [libva-intel-driver], you can also check to make sure VAAPI is working correctly by `vainfo` from [libva-utils].

The following output from `vainfo` shows that VAAPI is working:
```
vainfo: VA-API version: 1.5 (libva 2.5.0)
vainfo: Driver version: Intel i965 driver for Intel(R) CherryView - 2.3.0
vainfo: Supported profile and entrypoints
      VAProfileMPEG2Simple            :	VAEntrypointVLD
      VAProfileMPEG2Simple            :	VAEntrypointEncSlice
      VAProfileMPEG2Main              :	VAEntrypointVLD
      VAProfileMPEG2Main              :	VAEntrypointEncSlice
      VAProfileH264ConstrainedBaseline:	VAEntrypointVLD
      VAProfileH264ConstrainedBaseline:	VAEntrypointEncSlice
      VAProfileH264Main               :	VAEntrypointVLD
      VAProfileH264Main               :	VAEntrypointEncSlice
      VAProfileH264High               :	VAEntrypointVLD
      VAProfileH264High               :	VAEntrypointEncSlice
      VAProfileH264MultiviewHigh      :	VAEntrypointVLD
      VAProfileH264MultiviewHigh      :	VAEntrypointEncSlice
      VAProfileH264StereoHigh         :	VAEntrypointVLD
      VAProfileH264StereoHigh         :	VAEntrypointEncSlice
      VAProfileVC1Simple              :	VAEntrypointVLD
      VAProfileVC1Main                :	VAEntrypointVLD
      VAProfileVC1Advanced            :	VAEntrypointVLD
      VAProfileNone                   :	VAEntrypointVideoProc
      VAProfileJPEGBaseline           :	VAEntrypointVLD
      VAProfileJPEGBaseline           :	VAEntrypointEncPicture
      VAProfileVP8Version0_3          :	VAEntrypointVLD
      VAProfileVP8Version0_3          :	VAEntrypointEncSlice
      VAProfileHEVCMain               :	VAEntrypointVLD
```

After you installed it and have verified that VAAPI is working properly, add two lines to `$HOME/.config/chromium-flags.conf`:
```
--ignore-gpu-blacklist
--disable-gpu-driver-bug-workarounds
```

Then restart Chromium and go to `about:gpu`, if "Video Decode" is hardware accelerated then it works.

# Audio
Audio requires Intel SST firmware, which is taking away your freedom, but can be installed from linux-firmware package.

# Touchscreen
Requires [this silead firmware](https://github.com/onitake/gsl-firmware/blob/c180b35763433a61ca29740860940dc789c1b2e2/firmware/chuwi/hi10_plus/firmware.fw), put it to /lib/firmware/silead/gsl1680-chuwi-hi10plus.fw and reload the module.

Seems to work okay.

# What about.. gaming?
While I don't game much anymore, it's still fun to play games. Quake 3 and Extreme Tux Racer runs flawlessly. However Team Fortress 2 suffered from framerate issues, on low it's around 20 at 640x480.

It's not a gaming tablet so I don't expect much out of it, but hey, you get the idea.

# What about in daily use?
So far, it never let me down, I mainly use it to SSH to my home box and do work, and also I use it to work on postmarketOS and such.

It's great, while it's not powerful, it certainly did a great job.

Doing spreadsheets, writing documents or presentations should be fine, you can use LibreOffice if you don't want to pay for Office 365 (and having your privacy taken away).

# Issues
One of the issue is that even if the tablet is in suspend/sleep mode, it still waste quite a bit of battery for doing nothing, I assume that had something to do with the C-states, but I can confirm that one of my other friend which uses another laptop with the same CPU also got the same problem.

So I assume this is an issue with Linux's power management on this particular chipset.

Another problem is that when you hibernate the tablet, it saves content to swap, which is a normal thing. However when you power it back on, the tablet display stays off, and it seems to completely frozen.

The only thing I could do is to hard reset the tablet, which made me lost unsaved works.

# Should I buy this tablet?
If you're looking for a system to compile packages, gaming, or doing some intense work.. **this is not the system you're looking for, look for something way more better**.

[Arch Linux]: https://archlinux.org
[kernel.org]: https://kernel.org
[chromium-vaapi]: https://aur.archlinux.org/packages/chromium-vaapi
[chromium-vaapi-bin]: https://aur.archlinux.org/packages/chromium-vaapi-bin
[libva-intel-driver]: https://www.archlinux.org/packages/extra/x86_64/libva-intel-driver
[Big Buck Bunny]: https://peach.blender.org/download/
[libva-utils]: https://www.archlinux.org/packages/community/x86_64/libva-utils
