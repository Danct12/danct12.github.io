---
layout: post
title: My thoughts on Public Wi-Fi, and how safe is it?
---

Having Wi-Fi connectivity is very convenient, there's no point to bring a long wired Ethernet cord and plug it to your laptop, of course that's much faster than using Wi-Fi, but then it's not really portable at all.

And even then, most laptops nowadays doesn't come with Ethernet port so it can be more thinner, just take a look at the Pinebook/Pinebook Pro, and very recent Macbooks (and some Windows/FreeDOS laptops), you'll not get this functionality anywhere unless you have a dongle with you.

Enough talking about Ethernets, this is all about public Wi-Fi.

# The great of a Public Wifi
Now, you of course love the great, powerful computer at home, it's so good, it compiles Linux kernel under 10 minutes, or it's too good to play modern titles, all kind of stuffs.

But you also need to leave the house for some reason, such as going to [DEFCON] or any events, and carrying a laptop without internet isn't that great if you're a part of the social network or you just need to get some information from the internet.

This is when public Wi-Fi comes in, it enables you to use someone's Wi-Fi, for free (or at a cost). I believe some are guarded with a password, but maybe you can ask them for it.

# The bullshit of some Wi-Fi
Most of the time with public Wi-Fi, they ask you to visit the landing page of their hotspot, which asks you to click a button, or.. read the terms of service all that thing.

So let's take a look at a Wi-Fi I'm about to get to, this is at a convenicnce store.

![]({{ site.baseurl }}/images/PublicWifi/login-button.png)

Nothing out of ordinary, right? It's just a button telling you to connect the internet by clicking this button.

![]({{ site.baseurl }}/images/PublicWifi/login-info.png)

**SAY WHAT?** It asks you to put in your personal information. That's great, so much for privacy. 

There is no [Privacy Policy] page anywhere on this landing page! So you don't know where the hell this data will go, it goes to /dev/null? **Probably NOT**, you'll never know what they'll do.

They don't check for a valid phone number, so I put 10 digits of 9 and that's done.. Now what's next? Age? Well, I'll tell you that they also collect data from minors, disgusting.

And the rest, fill in with some invalid information, got off the hook, to the internet.

However, the other Wi-Fi I use, just need to click a button and that's it, you're on the internet.

# The danger
Now there are some risks involved when using public Wi-Fi, such as your traffic being captured and the data being stolen if it's on unencrypted HTTP, this approach will not work on HTTPS, which are encrypted.

However, they can still see the website you visits which is a part of DNS resolve (quick DNS change may get around this), but they'll not see the subdirs all of that stuff, so it's safe to do online shopping and you'll be perfectly fine.

# My thoughts?
This image pretty sums up my experience.

![]({{ site.baseurl }}/images/PublicWifi/Jerry.gif)

[DEFCON]: https://defcon.org/
[Privacy Policy]: https://en.wikipedia.org/wiki/Privacy_policy
