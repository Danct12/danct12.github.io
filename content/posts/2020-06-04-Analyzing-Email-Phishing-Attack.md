---
date: "2020-06-04T00:00:00Z"
title: Analyzing a password stealing email attachment
categories:
- Cybersecurity
tags:
- phishing
- email
- attachment
- malware
---

**Image hasn't moved over yet, so there are currently no images in this post.**

I'm sure all of you already have an email address, we usually use it so people can always contact me about things (or I contact you), and I'm sure you probably have (at least) one of these spam email, some are [419 scams], weird medicine ads and more.

BTW if you have emailed me about phone ports ETA and never heard anything back from me, it either means I haven't answered it or my email client filtered it (sorry, but I get alot of these emails), so these are better answered in [DanctNIX chat rooms].

# The email
Right, let's focus on what the title said, here's that email I received.

This email is in Chinese, but I know for a fact that you may not speak Chinese, so I've put it through a translator, here's the email in English.

```
Your account emailaddress@example.com password expires today 6/3/2020 12:33:33 p.m.

Please kindly use the button below to continue with the same password

See secure attached file.

NOTE: This is a one time user verification carried out in purpose to provide a more secured platform and shut down robot or malicious users
created in purpose of spamming or other fraudulent activities.
```

Below that is an attachment, with the name "PD.htm" (54.11 KB), not sure what PD is, Police Department? Let me know in the comments how you call it.

Inside the attachment, this is how the page looks like

And it looks like that the login page resemble a email login page from a very popular service in China (which is Netease), so in conclusion, it's a email phishing attack.

Any attempt to login via that page will yield `Password Authentication Failed!` which in reality your email is now stolen.

# Analyzing the source code
Opening the HTML page in a text editor gives you the following content:

In Javascript, what [atob] does is to decode a base64 string, and [unescape] is for decode a URL string, in short it is encoded twice.

So after we decoded the HTML attachment, here's a first look at how the information was sent through:

It uses smtpjs to send your email/password information over, and surprise, the SMTP information is all in plain text, it's not even encrypted or anything!

And after your information is sent, we can see that they also put a fake error, which is why we keep getting an error when trying to put the information in.

The rest of the page is just borrowed from the real login page, so there's nothing much to it.

# Inside the (phisher) mailbox
With the information gained in plain text, I decided to getting into the mailbox, and this is not very good..

Honestly, I don't want to take care of this so I decided to reach out to my another friend Umbra105 (Dong), he is known to took care of things like this, we've also reported the email to smtpjs which hopefully the address will get banned.

# Who were they targeting?
This email targets people that aren't tech savvy, or not good in cybersec (such as old people), most people will not fall into this and instead delete the email.

**And remember, emails like this does not come in a form telling you to open an attachment and magically verify the address, so be careful!**

# Special thanks
- Umbra105: for dealing with the phishing email/password and helps getting it taken down.

[419 scams]: https://en.wikipedia.org/wiki/Advance-fee_scam
[DanctNIX chat rooms]: https://github.com/DanctNIX/danctnix/blob/master/README.md#channel-list

[atob]: https://www.w3schools.com/jsref/met_win_atob.asp
[unescape]: https://www.w3schools.com/jsref/jsref_unescape.asp
