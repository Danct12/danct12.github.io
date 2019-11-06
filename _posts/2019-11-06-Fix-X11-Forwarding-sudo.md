---
layout: post
title: Fixing X11 Forwarding for sudo users
---

We probably don't use the root user to launch applications (security concerns), but in some cases we need to, and that's the case with programs like Zenmap, Etcher (accessing physical disks).

And we know that those applications launches perfectly fine locally, but sometimes we probably need to go outside, left our computer at home and all you got is a SSH server running on port [REDACTED].

You use your laptop (or your phone Linux Deploy + XServer XSDL) to connect to it, launch applications and work from there. But then when you just want to run a program as root, you can't because all you'll get is a very welcoming error:

![I JUST WANT TO RUN GNOME DISKS :(]({{ site.baseurl }}/images/X11Forwarding/ERROR.jpg)

## What the hell is going on can someone tell me please?
This happened because X11 authentication is based on cookies, each session is a randomized authorization cookie, and when you switch to another user (using su/sudo), this authorization cookie doesn't exist on that user.

From the man page for SSH, this is also mentioned:
```
     ssh will also automatically set up Xauthority data on the server machine.
     For this purpose, it will generate a random authorization cookie, store
     it in Xauthority on the server, and verify that any forwarded connections
     carry this cookie and replace it by the real cookie when the connection
     is opened.  The real authentication cookie is never sent to the server
     machine (and no cookies are sent in the plain).
```

## So, what can I do?
I assume you're already connected through SSH, right? If so, you'll have to get the current cookie for the current SSH session.
```
$ echo $DISPLAY
localhost:13.0
$ xauth list $DISPLAY
melttower/unix:13  MIT-MAGIC-COOKIE-1  9020db1e84384b27b45dff3e63c0b6af
```

So our current cookie for this session is:

`melttower/unix:13  MIT-MAGIC-COOKIE-1  9020db1e84384b27b45dff3e63c0b6af`

Now you'll need to add this cookie to the root user (or any user you want to forward X11 apps to):
```
$ sudo xauth add melttower/unix:13  MIT-MAGIC-COOKIE-1  9020db1e84384b27b45dff3e63c0b6af
```

After that, you should be able to run any X11 applications as sudo/su!

![much wow]({{ site.baseurl }}/images/X11Forwarding/Screenshot_2019-11-06_11-56-27.png)

Keep in mind that every time when you're disconnected from the session or start a new session, you'll have to do this everytime as the cookie is randomly generated.
