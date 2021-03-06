---
title: WiFi Infestations - Viral Wardriving
author: petko-d-petkov
date: Wed, 20 Feb 2008 12:04:54 GMT
template: this/views/post.jade
---

WiFi networks are the necessary evil. In this post I would like to briefly highlight some ideas on the potential damages that can be introduced when attackers combine automated viral-like attacks with human power. This post is largely related to the wifi worms topic that was quite present among all media outlets at the beginning of 2008. Although the proposed paper was quite theoretical, in this post I will try to prove that the introduced concepts are mostly practical when implemented with a twist.

Public WiFi networks are everywhere, especially today. We are surrounded by free hot spots, BT Openzone-s, office networks, ad-hoc networks like the infamous `hpsetup` printers, etc, etc, etc. WiFi is more accessible then ever and it seems like that this tendency will continue in the following years. In UK for example, BT's FON, a.k.a BT Openzone, is gaining a huge momentum. BT Openzone networks are everywhere. I know that Google is also working on similar projects, as well as many other companies do. The simple fact is that there is a lot of money to be made with free WiFi networks, often involving concepts like location based advertising, etc, but I will come to this some other time.

It is very important to understand that all WiFi networks are ruled by miniature devices. We call them embedded devices because they usually contain the entire package in a single box (software and hardware, i.e they are embedded). These devices are a vital part of the security and reliability properties of WiFi networks. However they fail to be secure or reliable. In the past couple of weeks, [here](/blog/router-hacking-challenge) in GNUCITIZEN, we've introduced numerous vulnerabilities that affect various types of embedded devices which are often used by SOHO companies, coffee shops, restaurants, etc. By war-driving around with a laptop equipped with all our findings, it is possible to spread a disease across numerous open WiFi networks. This is how WiFi worms could work.

It is not only one technology that can be attacked. There are several of them. Let's have a look at UPnP for example. Embedded devices like UPnP a lot. It is very simple to locate UPnP devices withing a network. All the attacker needs to do is to send several broadcast packets. Upon receiving them, UPnP enabled devices will piggy back with information about their UPnP interfaces. [Many UPnP devices allow unauthorized access](/blog/hacking-with-upnp-universal-plug-and-play) to critical features such as resetting the admin credentials, portforwarding and primary, DNS change, which is one of the keys to a successful WiFI worm attack. Simply put, if the attacker manages to change the default DNS of the WiFi access point, they will be able to permanently control the network where this device resides, i.e viral infection of a WiFi network.

DHCP also comes very handy for viral wardriving. I've discussed this before [here](/blog/r00ting-public-wifi-networks-dhcp-name-poisoning-attacks/), but let me summarize it one more time. The DHCP protocol allows you to register a name together with your IP. This means that anyone can register as many internal names as possible. Sometimes, it is even possible to register a name that maps to an external IP. Given the fact that a lot of setups use shortened names, such as proxy, mail, pop3, wpad in particular, home, intranet1/01, etc, and the fact that attackers can force the name to be present for a period of time such as 5 days, anyone who arrives on the WiFi network and uses shorten names somewhere on their setup, might get compromised. This conditions are met more often then you think.

[mDNS](/blog/name-mdns-poisoning-attacks-inside-the-lan/) is also a good technology to make use of when wardriving in order to propagate malicious code. mDNS is incredibly useful for locating devices but also to install such for further reference. For example, many video management interfaces rely on mDNS. If the attacker registers a new mDNS server and points it to an external resource, she will be able to effectively [hijack the video stream](/blog/hacking-video-surveillance-networks/). This injection often stays present until it is overwritten - something that rarely happens.

Various forms of injection attacks can also take place. I've started a discussion over [here](/blog/dhcpmdns-injection-issues/) but I would like to elaborate further. Because most embedded devices come with some sort of web-based management interface, and because these web interfaces are prone to all sorts of injection issues, attackers can trivially install persistent XSS vectors. For example, when you register a name through DHCP, this information is usually displayed on the front page of the admin console where all other clients are listed. However, through DHCP attackers can register names that contain special characters such as `<` and `>`. This means that it is trivial to backdoor the remote devices with a persistent XSS vector which will give further access to the device management interface once an authorized user visits the infected page.

> Many devices come with SIP ports open as well. Every single SIP INVITE request me be recorded without being sanitized, therefore allowing attackers to persistently backdoor the device management console. Keep in mind that this is also applicable to any device that has SIP functions exposed on the Internet.

	INVITE sip:UAB**<injection point>**@example.com SIP/2.0
	Via: SIP/2.0/UDP 10.20.30.40:5060
	From: UserA**<injection point>** <sip:UAA**<injection point>**@example.com>;tag=589304
	To: UserB**<injection point>** <sip:UAB**<injection point>**@example.com>
	Call-ID: 8204589102**<injection point>**@example.com
	CSeq: 1 INVITE
	Contact: <sip:UserA**<injection point>**@10.20.30.40>
	Content-Type: application/sdp
	Content-Length: 0

_These are just a few of the possible scenarios which are not that difficult to implement, as there are more then enough tools to ease the process. Viral WiFi attacks based on simple wardriving is very much possible._
