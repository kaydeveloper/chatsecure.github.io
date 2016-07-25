---
layout: post

title: ChatSecure iOS v3.2.3 - XMPP Push
category: blog

author:
  name: Chris Ballinger
  twitter: chrisballingr
  gplus: 110173710196322914492 
  bio: Founder & Lead Developer
---

# ChatSecure iOS v3.2.3 - XMPP Push

We're excited to announce that XMPP push ([XEP-0357](http://xmpp.org/extensions/xep-0357.html)) is now available, finally allowing users to receive push messages from any contact. This feature is only available when used with compatible XMPP servers, and requires special modules to be enabled for Prosody ([`mod_cloud_notify`](https://modules.prosody.im/mod_cloud_notify.html)) or ejabberd ([`mod_push`](https://github.com/royneary/mod_push)). 

Our next release will focus on [OMEMO](https://conversations.im/omemo/) support for multi-device asynchronous end-to-end encryption, which will provide huge usability gains over OTR on mobile devices. Thankfully the GPL + App Store licensing issues concerning SignalProtocol have been [resolved](https://whispersystems.org/blog/license-update/). You can try OMEMO today in other apps such as Conversations, Gajim, and Cryptocat.

v3.2.3 changes:

* XMPP push for supported servers (XEP-0357)
* Improved subscription requests UI
* Basic vCard nickname support
* Fix issues with missing messages during stale OTR sessions
* Improved IPv6 support for NAT64/DNS64
* Fix some issues with presence/availability
* Added button to view your password
* Fix issue where message view would appear multiple times
* Automatically start OTR sessions when contact is online
* Send error messages back to contact when messages cannot be decrypted

[Download](https://itunes.apple.com/us/app/chatsecure/id464200063) on the App Store.