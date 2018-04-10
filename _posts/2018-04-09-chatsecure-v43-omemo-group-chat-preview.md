---
layout: post

title: ChatSecure v4.3.0 - OMEMO Group Chat Preview
category: blog

author:
  name: Chris Ballinger
  twitter: chrisballingr
  gplus: 110173710196322914492 
  bio: Founder
---

# ChatSecure v4.3.0 - OMEMO Group Chat Preview

![California Sunset](/images/california-sunset.jpg)

Chat history now automatically synchronizes between your devices - including OMEMO chats! This includes any device using a modern XMPP client that supports Message Archive Management (aka MAM or [XEP-0313](https://xmpp.org/extensions/xep-0313.html)). There still may be some rough edges with some configurations (like duplicate messages), but if your server supports MAM, you should be good to go. You'll also notice that your active group chats are synchronized between devices via support for Group Chat Bookmarks ([XEP-0048](https://xmpp.org/extensions/xep-0048.html)).

Another big change is preliminary support for OMEMO Group Chats. This still needs some testing and isn't yet recommended for general use. If you'd like to try it, you must first enable it via the Advanced section of the Settings screen, and then also enable it individually for each group chat in the Members screen. Regardless of the settings you will still be able to receive incoming group OMEMO messages.

Up next will be a performance and stability release focusing on MAM and OMEMO groups.

### Contributing

Thank you to all of the monthly supporters! 

Not a supporter yet? It's easy! You can start supporting development directly in the app.  [Sustainable open source starts with you](https://chatsecure.org/blog/sustainable-open-source-starts-with-you/)! ❤️

##### Download the latest ChatSecure version here:

[![download chatsecure on the app store](https://chatsecure.org/images/appstore.svg)](https://itunes.apple.com/us/app/chatsecure/id464200063)

### Release Notes

* Message Archive Management (XEP-0313) - one-to-one and group chat history is now synchronized between multiple devices, if supported by your server.
* Group Chat Bookmarks (XEP-0048) - Group chats are now bookmarked on your server to allow persistence between devices / installs.
* OMEMO Group Chat Encryption Preview - This is not yet recommended for general use and is for advanced users only. Must be globally enabled in Advanced Settings as well as individually for each group chat.
* Improvements to general group chat user experience
* Bug fixes and performance improvements
* [Full release notes](https://github.com/ChatSecure/ChatSecure-iOS/releases/tag/v4.3.0)
* [Changelog](https://github.com/chatsecure/chatsecure-ios/compare/v4.2.1...v4.3.0)