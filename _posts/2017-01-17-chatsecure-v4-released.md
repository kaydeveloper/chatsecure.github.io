---
layout: post

title: ChatSecure v4.0 - OMEMO and Signal Protocol 
category: blog

author:
  name: Chris Ballinger
  twitter: chrisballingr
  gplus: 110173710196322914492 
  bio: Founder & Lead Developer
---

# ChatSecure v4.0 - OMEMO and Signal Protocol

We're excited to announce the release of ChatSecure v4.0, our largest step forward in usability since the addition of push messaging six months ago. The most significant new feature is [OMEMO Encryption](https://en.wikipedia.org/wiki/OMEMO), a mobile-friendly encryption scheme pioneered by [Conversations](https://conversations.im) that adapts [Signal Protocol](https://en.wikipedia.org/wiki/Signal_Protocol) to the XMPP world.

Using [OTR](https://en.wikipedia.org/wiki/Off-the-Record_Messaging) on mobile has always been problematic because it was designed for desktop computers and synchronous conversations. For example, if you don't have an active OTR session, you can't start a new secure session if your contact is offline. Even if you do have an OTR session, it can go stale if one of the sides is purged from RAM due to low memory. This can lead to messages that disappear into the ether with no standardized way for the recipient to indicate which message they couldn't decrypt.

OMEMO fixes all of these problems, and opens doors to new features that were impossible with OTR, like multi-client support, encrypted group chat, and more reliable file transfers. Multi-client conversations would work particularly well with our planned Desktop client, so we're excited to add support for these features in a future releases.

There are some other major changes in this release that improve the user experience, such as the outgoing message queue and enhanced identity management. The message queue automatically negotiates OMEMO and OTR sessions and allows you to resend messages in case of failure.

![Image of Profile View](/images/v4-profile.png)

The new profile view allows you to view a contact's OMEMO and OTR fingerprints, change each fingerprint's trust settings, and modify the default encryption method. We've made important changes to the way trust is handled for new contacts by adopting the [TOFU](https://en.wikipedia.org/wiki/Trust_on_first_use) or "trust on first use" model. The first time you see OMEMO or OTR fingerprints for a contact, they will appear as trusted and marked with "TOFU" in the user interface. Any subsequent fingerprints will be untrusted and need to be manually verified. In this release you can compare fingerprints out-of-band by pressing on the cell and bringing up the system share dialog, but we plan to streamline the fingerprint comparison process in the future.

There are [hundreds of other changes](https://github.com/chatsecure/chatsecure-ios/compare/v3.2.3...v4.0) under the hood that fix bugs, improve performance, and enhance reliability. On the roadmap for v4.1 and beyond are improvements to group chat, including OMEMO encryption, multi-device chat history synchronization ([XEP-0313 MAM](http://xmpp.org/extensions/xep-0313.html)), read receipts (aka chat markers [XEP-0333](http://xmpp.org/extensions/xep-0333.html)), improved file transfer, and more. 

We're excited to see people experience this new frontier for XMPP usability. We will be working with the Zom project to bring OMEMO support to their suite of apps, and we expect other apps will start adopting OMEMO as well. 

Thank you to everyone who helped make this release a reality!

[![Download on the App Store](/images/appstore.svg)](https://itunes.apple.com/us/app/chatsecure/id464200063)

[Download ChatSecure on the App Store](https://itunes.apple.com/us/app/chatsecure/id464200063)