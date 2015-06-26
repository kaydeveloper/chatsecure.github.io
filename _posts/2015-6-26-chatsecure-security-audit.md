---
layout: post

title: ChatSecure iOS Security Audit
category: blog

author:
  name: Chris Ballinger
  twitter: chrisballingr
  gplus: 110173710196322914492 
  bio: Lead Developer
---

# ChatSecure iOS Security Audit

Last year [OpenITP](https://openitp.org) generously funded a [security audit](http://blog.quarkslab.com/security-assessment-of-instant-messaging-app-chatsecure-when-privacy-matters.html) of the ChatSecure iOS client, performed by [QuarksLab](http://www.quarkslab.com) in Q1 2014. It was the first professional security audit of the code and it revealed a few critical issues that we were able to quickly address.

Originally ChatSecure was designed to be a multiprotocol IM client that supported OTR over AIM, Google Talk, Facebook, and generic XMPP. Because [libpurple](https://developer.pidgin.im/wiki/WhatIsLibpurple), used in Pidgin and Adium for chat network support, is licensed under GPL we could not distribute it on the App Store. Additionally libpurple has had [quite a few vulnerabilities](http://www.cvedetails.com/vulnerability-list/vendor_id-6938/product_id-11666/Pidgin-Pidgin.html) itself,  so instead we chose to use two Objective-C libraries: [XMPPFramework](https://github.com/robbiehanson/XMPPFramework) for GTalk, Facebook and XMPP, and a lesser-known library called [LibOrange](https://github.com/unixpickle/LibOrange) for AIM support. 

## XMPP and STARTTLS

One of the issues they found was the ability for an attacker with a privileged network position to potentially block the [STARTTLS](https://en.wikipedia.org/wiki/STARTTLS) functionality of XMPP, which is used to initiate TLS connections. Although we support TLS with certificate pinning, XMPPFramework directly followed the XMPP specification which states the server is to specify (in plaintext) whether or not TLS is supported or required. This is a [problem for all protocols utilizing STARTTLS](https://www.agwa.name/blog/post/starttls_considered_harmful) (including email), and no server should ever allow plaintext connections in 2015. We [worked with the XMPPFramework maintainers](https://github.com/robbiehanson/XMPPFramework/commit/db291a40e2135d82f07ca4350259e7225a3db7b4) to add the ability to require TLS connections regardless of what the server reports. This way if an attacker tries to force a downgrade attack, the connection simply fails.

Many XMPP server operators have [pledged to require STARTTLS](https://raw.githubusercontent.com/stpeter/manifesto/master/manifesto.txt) for all client-to-server and server-to-server connections. Due to this change, many servers no longer federate with Google's XMPP gateway because [Google still doesn't support server-to-server STARTTLS](https://rachelbythebay.com/w/2012/05/22/s2s/).

## LibOrange and AIM

LibOrange (for AIM/Oscar) was originally included back in 2011 when ChatSecure (then called "Off the Record") was a proof of concept pre-release hobby project to demonstrate libotr on iOS. The LibOrange code originally was not carefully audited and turned out to contain serious flaws in both its memory handling, and the [example implementation](https://github.com/unixpickle/LibOrange/blob/master/LibOrange/MyTest.m), which included debugging commands that were not documented or fully understood.

Although we had been planning to remove AIM support for other reasons, thanks to Quarkslab we immediately removed LibOrange and AIM support and pushed a new release as soon as these flaws were uncovered on 2/21/2014. Fortunately there were no complaints from our users after its removal.

If you still use AIM on other chat clients, you should disable it immediately and migrate to other networks. AIM is a centralized messaging service [hosted in the US](https://eff.com/ar/document/aol-law-enforcement-guide), and has a complete view of your message content, history, contacts, and metadata (IP address, connection/disconnection times, etc). Using OTR over AIM only helps protect message content.

## Improving Security

Since the audit last year, [we have implemented a number of features](https://chatsecure.org/blog/chatsecure-ios-v3-released/) to improve security. For example, all content is locally encrypted in a SQLCipher database, and it is possible to connect to XMPP servers over Tor.

XMPP servers with a Tor `.onion` address that force OTR, such as [Caylx](https://www.calyxinstitute.org/projects/public_jabber_xmpp_server) or [otr.im](https://otr.im/chat.html), currently offer the one of the easiest ways to protect both message content and identifiable metadata.

Even better is to physically host an XMPP server for yourself and your friends, but unfortunately this is still very difficult to get right, even for tech savvy users.

The combination of XMPP+OTR+Tor still offers the best and easiest way to provide decentralization, content/metadata protection, and censorship resistance. Unfortunately this combination is difficult to make user-friendly, especially on mobile devices. Both XMPP and OTR were originally designed for desktop computers and are definitely showing their age in the age of mobile.

There are efforts to replace this combination, such as [Pond](https://pond.imperialviolet.org), but it's almost impossible for a non-technical person to understand or setup.

If you don't need decentralization or metadata protection, [TextSecure](https://play.google.com/store/apps/details?id=org.thoughtcrime.securesms)/[Signal](https://itunes.apple.com/us/app/signal-private-messenger/id874139669) is a very good choice because it is easy to setup for non-technical users and works very well on mobile. Its main downside is that you still need to use a real phone number to register, and to communicate with other people you need to share your phone number with them, which is not always desirable. It also makes open federation impossible.

## Moving Forward

We are still committed to supporting the XMPP+OTR+Tor combination in ChatSecure for now, but are monitoring the maturity of new technologies that solve usability headaches without sacrificing decentralization, content/metadata protection, and censorship resistance. We are working on a solution for interoperable push messaging in ChatSecure, XMPP will also soon finally have a way to provide mobile push notifications, and Axolotl (which underlies Signal/TextSecure) has proven to be a great replacement for OTR on mobile devices.

Although open source software with deterministic builds remains a best practice for security software, careful coding techniques cannot always protect against all flaws, especially when linking against 3rd party libraries. We will be commissioning a new professional security audit of the ChatSecure iOS and Android code to be completed by the end of the year.