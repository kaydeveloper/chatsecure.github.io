---
layout: post

title: ChatSecure v2.2 Released
category: blog

author:
  name: Chris Ballinger
  twitter: chrisballingr
  gplus: 110173710196322914492 
  bio: Lead Developer
---

ChatSecure v2.2 for iOS was [approved by Apple today](https://itunes.apple.com/us/app/chatsecure/id464200063). One of the main new features is support for [SSL certificate pinning](https://en.wikipedia.org/wiki/Transport_Layer_Security#Certificate_pinning), to help prevent man-in-the-middle attacks. A nice side effect of implementing this feature is that we now support alternative root CAs like [CACert.org](http://www.cacert.org), which now means [jabber.ccc.de](http://web.jabber.ccc.de) accounts should work properly. This also means that if you run your own XMPP server with a self-signed certificate, you should have less problems connecting and can now verify and pin the [SHA1 hash](https://en.wikipedia.org/wiki/SHA-1) of your certificate before connecting. [@davidchiles](https://github.com/davidchiles) crafted a beautiful and simple interface that appears for each new certificate, including information about whether or not the certificate would pass the built-in iOS certificate checks:

![SSL Pinning Support](/images/ssl_pinning.jpg)

We also implemented another highly requested feature: you can now enable automatic login for your accounts. Coming soon is support for [Tor](https://www.torproject.org), [SOCKS5](https://en.wikipedia.org/wiki/SOCKS#SOCKS5), and XMPP account creation ([XEP-0077](http://xmpp.org/extensions/xep-0077.html)).

### Notable Changes

* XMPP: SSL Certificate Pinning
* XMPP: Support for non-standard root CAs like CACert to support jabber.ccc.de
* XMPP: Better support for self-signed SSL certificates via certificate pinning
* Support auto-login for accounts
* User interface improvements
* Security improvements
* Internal refactoring and code cleanup
* Fix many crashes
* Update 3rd party libraries
* [Full Changelog](https://github.com/chrisballinger/Off-the-Record-iOS/compare/v2.1.2...v2.2)

Special thanks to [@vitalyster](https://github.com/vitalyster) for the UI patches included in this version.

### Download

Download it for free on the [App Store](https://itunes.apple.com/us/app/chatsecure/id464200063) and check out the [source code](https://github.com/chrisballinger/Off-the-Record-iOS/releases/tag/v2.2) on GitHub.