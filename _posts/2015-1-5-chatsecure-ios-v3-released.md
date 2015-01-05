---
layout: post

title: ChatSecure iOS v3.0 Released
category: blog

author:
  name: Chris Ballinger
  twitter: chrisballingr
  gplus: 110173710196322914492 
  bio: Lead Developer
---

## ChatSecure iOS v3.0 Released

Over the last year, [David Chiles](https://github.com/davidchiles) and I have been working on a major overhaul of the iOS app to modernize the user experience and incorporate additional security features. The most significant user-facing changes are:

* The buddy list has been replaced by a list of your most recent conversations, bringing it in line with modern messaging clients.
* Conversation archives are encrypted using [SQLCipher](https://www.zetetic.net/sqlcipher/).
* Experimental [Tor](https://en.wikipedia.org/wiki/Tor_(anonymity_network)) support for custom XMPP accounts.

[Download ChatSecure](https://itunes.apple.com/us/app/chatsecure/id464200063) for free from the App Store. If you're a developer you can also [compile it yourself from the source code on GitHub](https://github.com/chrisballinger/ChatSecure-iOS).

### Tor Support 

Right now (to my knowledge) we are the only messaging app on the App Store that supports Tor. Although the current implementation appears to be functional, please only use it for testing purposes until it has been studied further by security professionals. In other words, **do not rely on it for strong anonymity**, and use something like [TAILS](https://en.wikipedia.org/wiki/Tails_(operating_system)) instead.

During our journey to add Tor support, we first tried to extract the Tor management code from [Mike Tigas](https://twitter.com/mtigas)'s [Onion Browser](https://github.com/OnionBrowser/iOS-OnionBrowser), but discovered it was too tightly coupled with the rest of the app. We also investigated [Tor.framework](https://github.com/hivewallet/Tor.framework) by [Hive Wallet](https://www.hivewallet.com) but it required some awkward patching of the Tor source code, and has since been deprecated by the original developers. Eventually we discovered [Claudiu-Vlad Ursache](https://twitter.com/ursachec)'s [CPAProxy](https://github.com/ursachec/CPAProxy), a more modern attempt at a thin Objective-C wrapper around Tor's control port. Although it is currently missing a few features like customizable bridges and pluggable transports (and a security audit), I would encourage other developers who are interested in adding Tor support to their iOS apps to help us improve CPAProxy.

### Encrypted Storage

When ChatSecure iOS v2.0 was released over a year ago, it contained a major overhaul of the internal data model to support [Core Data](https://en.wikipedia.org/wiki/Core_Data), Apple's solution for data persistence. We originally planned on utilizing the MITRE Corporation's [encrypted-core-data](https://github.com/project-imas/encrypted-core-data) project, which adds a customized `NSPersistentStoreCoordinator` backed by Zetetic's [SQLCipher](https://www.zetetic.net/sqlcipher/). Unfortunately working with Core Data can be terribly frustrating, especially when you cannot debug its closed-source internals.

Fortunately we discovered [YapDatabase](https://github.com/yapstudios/YapDatabase) by [Robbie Hanson](https://github.com/robbiehanson), an Objective-C key-value-collection store built on top of [sqlite](http://www.sqlite.org). It has all sorts of nice features like a coherent concurrency model, fast full text search, easy binding to `UITableView`, and more. If you develop iOS apps, I strongly encourage you to check it out, especially in conjunction with something like [Mantle](https://github.com/mantle/mantle). Because it is built on top of sqlite, it was relatively straightforward for us to add SQLCipher support (use the `YapDatabase/SQLCipher` [Cocoapods](http://cocoapods.org) subspec).

### New User Interface

Our overhaul of the UI started at the [OpenITP UX Sprint](https://openitp.org/openitp/ux-sprint-for-security-privacy-tools.html), which brought together developers and designers to help improve the usability of crypto tools. One of the biggest challenges when creating security software is ensuring it's usable by normal humans. During this event we decided to finally move away from the "buddy list" because it no longer reflects how people use messaging apps, especially on mobile. In its place, we added the "Conversations" view, which simply lists your most recent conversations and is designed to feel similar to the built-in iOS Messages app.

We also decided to use [Jesse Squires'](http://www.jessesquires.com) totally awesome [JSQMessagesViewController](https://github.com/jessesquires/JSQMessagesViewController) for the messaging UI. We were previously using a custom solution designed to imitate the iOS 6 Messages.app, but this new approach should allow us to more easily add in-line media messaging in the future.

### On the Roadmap

This release has a large amount of internal refactoring that should (hopefully) make it easier to maintain and add new features. Here are some features we are planning on adding over the next year:

* Inline multimedia messaging via [OTRDATA](https://dev.guardianproject.info/projects/gibberbot/wiki/OTRDATA_Specifications)
* A modern onboarding experience that makes it easier for new users to get started
* More options for users behind restrictive firewalls ([Tor pluggable transports](https://www.torproject.org/docs/pluggable-transports.html.en))
* An interoperable [privacy-conscious solution for push messaging](https://github.com/ChatSecure/ChatSecure-Push-Server/blob/master/docs/v3/README.md)
* [Axolotl](https://whispersystems.org/blog/advanced-ratcheting/), the mobile-friendly asynchronous encryption protocol used by TextSecure
* Internet-free hyperlocal [chat network over Bluetooth LE](https://github.com/chrisballinger/BLEMeshChat)
* Sandboxed Mac OS X port
* An easy way for users to set up their own XMPP server

Unfortunately, despite the recent proliferation of "secure messaging" apps, we are still a long way from ubiquitous, easy to use, decentralized, verifiable end-to-end encryption.