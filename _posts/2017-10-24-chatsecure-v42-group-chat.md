---
layout: post

title: ChatSecure v4.2.0 - Group Chat
category: blog

author:
  name: Chris Ballinger
  twitter: chrisballingr
  gplus: 110173710196322914492 
  bio: Founder
---

# ChatSecure v4.2.0 - Group Chat

![California Coastline](/images/california-coast.jpg)

First of all, thank you to all of the monthly supporters! Your contributions have been a great motivator to keep the release cycle moving along at a regular pace, from master branch, to TestFlight, to App Store. Not a supporter yet? It's easy! You can start supporting development directly in the app. Remember, [sustainable open source starts with you](https://chatsecure.org/blog/sustainable-open-source-starts-with-you/)! ❤️

This version contains numerous improvements to the existing group chat functionality: unencrypted media transfers (XEP-0363), brand new participant list, and enhanced stability and reliability. There is still a lot of work to be done, but it has stabilized enough for a general release. It was designed with small, private groups in mind, so it hasn't been tested with very large groups, and "anonymous" groups are currently unsupported.

Up next is support for [XEP-0313: Message Archive Management](https://xmpp.org/extensions/xep-0313.html), which will allow you to use the same account on multiple devices, and is a prerequisite for OMEMO group chats.

##### Download the latest ChatSecure version here:

[![download chatsecure on the app store](https://chatsecure.org/images/appstore.svg)](https://itunes.apple.com/us/app/chatsecure/id464200063)

### Release Notes
* Improved group chat reliability
* Media sharing in group chats (unencrypted only)
* Redesigned group participants view
* Improve performance of chat view. Thanks @stigger!
* Bug fixes and refactoring
* Tor 0.3.0.11

Changelog: https://github.com/chatsecure/chatsecure-ios/compare/v4.1.0...v4.2.0
