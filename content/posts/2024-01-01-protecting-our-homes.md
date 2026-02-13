---
date: 2024-01-01T00:00:00-05:00
slug: "protecting-our-homes"
title: "Protecting our homes"
categories: Internet
---
We want our homes to be safe. Many people suffice with a heavy door and a strong lock. But it isnâ€™t always enough to fortify our homes. In our increasingly volatile world, it is wise to strengthen our selves, with firearms and the like. But even the most ardent believers in the importance of self defense donâ€™t recommend removing your front door.

The internet is good, bad, everywhere, and forever. Most people recognize the importance of restricting access to dangerous content on devices, even if they canâ€™t be bothered to do anything about it. It is a challenge to set up filters on all of our familyâ€™s myriad devices, and there are often monthly fees attached. It has the potential to get confrontational, and even after all of that, itâ€™s only for devices we know about.

All the discussion of devices and filters is only about those particular devices. In regards to our internet itself, we donâ€™t even have a door to close. Maybe we comfort ourselves with a network password, as if there arenâ€™t simple ways to get it (if it isnâ€™t given outright). We hope for the best and donâ€™t give it any thought.

The internet is full of dangerous places. There is research demonstrating the mental harm even of over exposure to safe, benign websites (as if we needed to be told). It is shocking how we can be so callous as to have a network in our homes, and not even care enough to know whatâ€™s being done with it, or apply even the most modest of limitations to it.

We bring the internet into our homes. We pay the bills. Shouldnâ€™t we be in charge of it? Why do we let it run its course, as if itâ€™s an unstoppable force of nature?

Wouldnâ€™t it be wonderful if we could see all devices on our internet and what websites they are visiting? If our internet itself would block dangerous web sites, and set schedules and connection limits for everything else. If a new device connects to our internet, it would tell us, and we could choose how it gets handled. And all without installing anything on any of our devices.

All of that is possible, and you can probably do a lot of that already with the router you have in your house. Itâ€™s worthwhile to look into.

Most name-brand routers, such as [Google nest](https://support.google.com/googlenest/answer/7197116?hl=en), [Amazon eero](https://blog.eero.com/introducing-eeros-latest-feature-family-profiles/), and [many others](https://www.lifewire.com/best-parental-control-routers-4160776), have well regarded parental controls. One family of devices I used for a time was [Gryphon](https://gryphonconnect.com/collections/all), but I moved away from them because of reliability issues and internet speed, and no longer recommend them.

Another option is to get a dedicated device which is designed specifically to simplify internet management. An example would be one of the dedicated firewalls from [firewalla](https://firewalla.com/products/firewalla-purple-se). Firewalla sells a variety of devices, depending on how fast your connection is. There are no subscription fees, and [they are highly regarded](https://www.pcmag.com/reviews/firewalla).

A brief, simplified refresher on some networking hardware terms:

*   A modem connects to the internet
*   A router connects to a modem, and sends a wifi signal to your house
*   Some modems are all in one units, and are also routers. Even in such a case, you could connect a router to it, and use that instead (although you would probably have to login to your modem and put it in to something called bridge mode)
*   A firewall can be a dedicated device which is connected to your network, which can block unwanted network activity.

Installing a firewalla is easy if you already own a dedicated router; connect the router to the firewall, and the firewall to the modem. If you donâ€™t own a dedicated router, you can can get a used router on ebay for next to nothing. (If you have to use an all in one modem/router, setup [may be simple](https://help.firewalla.com/hc/en-us/articles/115004292514-How-does-Firewalla-Intercept-Traffic-#h_01F8F0BBM94B8RC4TPPGZXPKQ5), or a [little bit more complicated](https://help.firewalla.com/hc/en-us/articles/115004292514-How-does-Firewalla-Intercept-Traffic-#h_01F8F096AGV8FW7K1D673AJEQ6), depending [on the device](https://help.firewalla.com/hc/en-us/articles/360047098773).)

Once you have the firewall connected to your network and have management set up on your smart phone with [their app](https://play.google.com/store/apps/details?id=com.firewalla.chancellor&hl=en_US&gl=US) (also available [on iOS](https://apps.apple.com/us/app/firewalla/id1180904053)), you are in control of your internet.

It is beyond the scope of this article to write how to use the firewall, but here are some things you can do:

*   Block websites, or categories of websites, from all devices
*   Create rules for individual devices, or groups of devices
*   Decide how to handle devices you donâ€™t recognize. Maybe you want to block them, or just give them a very slow connection, or limit what they can do. Or some combination of that.
*   Control which hours of the day particular devices or groups can connect to the internet, or to particular categories of websites, or to particular websites.
*   Know whatâ€™s going on â€“ which websites are being visited, how much data is being downloaded, etc.

You can even have devices always connect to your firewall, even if theyâ€™re on another internet connection, using a [VPN server](https://help.firewalla.com/hc/en-us/articles/115004274633-Firewalla-VPN-Server).

Another device which can probably do anything the firewalla can (and more) for cheaper (or free, if you have an older laptop you can set it up on) is [pfSense](https://shop.netgate.com/products/1100-pfsense). The thing to note about pfSense is that it is enterprise grade business software, used to protect large corporations and websites. If someone wants to go that route, they offer [training and certification](https://www.netgate.com/training/pfsense-fundamentals-and-advanced-application), but I expect itâ€™ll be a lot more time and effort then youâ€™re planning on, unless youâ€™re an IT professional.

There are no shortage of options, the main thing is to choose something and see if it works for you. The internet is here. Take charge.

Addendum â€“ Device Filters
-------------------------

Controlling the network is not a replacement for filters on devices. There are some things which, for technical reasons, are very easy to do in a program installed on a device, and impossible, or very difficult (or dangerous, from a security perspective) to do on a router or firewall.

For example:

1.  Blocking a particular features of an app (for example, whatsapp channels)
2.  Blocking particular parts of a webpage
3.  Blocking only some areas of a website
4.  Filtering based on screen contents
5.  Filtering no matter what internet connection youâ€™re on. (This is possible with some firewall solutions using a VPN, but requires additional setup, and some app blocks to prevent the VPN from simply being disabled)

A router or firewall is categorically incapable of doing any of that, except in those cases where it can do so with the only blocking trick they have: blocking websites. As someone is browsing the web (or using an app which is querying specific websites for data behind the scenes), the only thing that the router or firewall can see is the name of the websites which are being accessed. Everything else is encrypted and hidden. (Technical note: I suspect that with pfSense you can set up a man in the middle and shared certificate, and then filter based on content. But that takes a lot of know how. If someone tries to do that without _really_ knowing what theyâ€™re doing, theyâ€™re probably just going to get themselves hacked.)

As this implies, they rely on up-to-date lists of website names and category in order to be useful. In general, vendorsâ€™ lists are more than comprehensive enough, and you can always add rules for anything additional that they may have missed.

(When it comes to websites dedicated to inappropriate content in particular, a router or firewall can be configured to use a DNS service called [OpenDNS family shield](https://support.opendns.com/hc/en-us/articles/360038086532-Using-DNS-over-HTTPS-DoH-with-OpenDNS), which practically speaking categorizes the entire internet. The details of setting that up (or what that means) are outside the scope of this article.)

Another useful feature of device filters is limiting the total amount of time allowed to use an app. You can set schedules on a router or firewall, for example that anash.org canâ€™t be accessed from 1-3PM). Setting a more general time limit, for example that you can only spend an hour on anash.org a day, is something that they wonâ€™t generally be able to support. Firewalla is [starting to support that](https://help.firewalla.com/hc/en-us/articles/22912094066707#h_01HFA581R69C8SRJSE0N2ZRHQC) on specific apps, which is a significant technical achievement on their part. They arenâ€™t even trying to add more general support for that, a feature which most device filter software is able to easily implement.

For all of their qualities, device filters have some key weaknesses. To reiterate, they have to be installed. And they canâ€™t be installed on devices you donâ€™t know about, or thought you had meant to throw out and stuffed in a drawer. In addition to those weaknesses mentioned earlier, donâ€™t forget that with sufficient determination, you can probably get around them. Iâ€™m not knowledgeable about them, but I strongly suspect that when I write probably Iâ€™m being very generous.

This is true to a much greater degree with device filters than router/firewall filters. If youâ€™re internet is filtered, it wonâ€™t give you access to blocked websites. Those websites might as well not exist. You canâ€™t get not kosher food from your fridge because it never even enters your house. The same applies when you put a filter on the internet connection itself.

Addendum â€“ VPNs
---------------

VPNs are a larger topic that I wonâ€™t go into detail about here. Some important pointers:

1.  Make sure the VPN is configured to be always active (for all internet connections â€“ mobile data and all wifi networks).
2.  Install an app to block access to device settings (such as the free [Norton app lock](https://play.google.com/store/apps/details?id=com.symantec.applock)), otherwise anyone using the phone can just disable the VPN connection. I donâ€™t know how that works on iOS, but in general Iâ€™ve heard that iOS has excellent parental controls built in, so Iâ€™m sure itâ€™s possible.