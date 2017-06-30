---
layout: post

title: ChatSecure v4.1.0 - Media Messaging
category: blog

author:
  name: Chris Ballinger
  twitter: chrisballingr
  gplus: 110173710196322914492 
  bio: Founder
---

# ChatSecure v4.1.0 - Media Messaging

![OMEMO file transfer](/images/omemo-file-transfer.png)

This release contains major improvements to how media messages are handled. We've added support for both [XEP-0363: HTTP Upload](https://xmpp.org/extensions/xep-0363.html) and the [aesgcm:// scheme](https://github.com/iNPUTmice/ImageDownloader), allowing for mobile-friendly asynchronous end-to-end encrypted file transfers.

Previously we used a rather obscure protocol called [OTRDATA](https://dev.guardianproject.info/projects/gibberbot/wiki/OTRDATA_Specifications) that utilized [OTR TLVs](https://otr.cypherpunks.ca/Protocol-v3-4.0.0.html) to send arbitrary data through existing OTR sessions. It worked reasonably well... sometimes. It was subject to throttling by XMPP servers, had a lot of encoding overhead, and wouldn't work unless both parties were online and were in an active OTR session.

This new file transfer mechanism was designed to work well with OMEMO, and should handle multiple devices and group chats once that work is completed. To see if your server supports XEP-0363, check the "Server Information" section of your account details. If not, contact your server administrator or in the meantime test it out on a server [from this list](https://gultsch.de/compliance_ranked.html).

Up next will be improvements to group chat, multi-device conversation history, and better reliability of push notifications. If you like what we're doing, don't forget that [sustainable open source starts with you](https://chatsecure.org/blog/sustainable-open-source-starts-with-you/)! Thank you so much to everyone who has pledged their support! ❤️

##### Download the latest ChatSecure version here:

[![download chatsecure on the app store](https://chatsecure.org/images/appstore.svg)](https://itunes.apple.com/us/app/chatsecure/id464200063)

# What's new in 4.1.0
* [XEP-0363](https://xmpp.org/extensions/xep-0363.html): HTTP Upload support for much faster and reliable media messaging. [1]
* [XEP-0352](https://xmpp.org/extensions/xep-0352.html): Client State Indication. Helps reduce network usage when running in the background.
* End-to-end encryption for file transfers in OMEMO or OTR sessions [2].
* Inline media previews for incoming URLs. (Optional)
* Bug fixes and refactoring.
* Tor 0.3.0.9

# Caveats
* Your server administrator must enable support for XEP-0363. See mod_http_upload for Prosody [3] and ejabberd [4] for more details.
* Encrypted file transfer is required in OMEMO/OTR, but has limited compatibility for receiving clients. Users on the other end will receive `aesgcm://` links [2].
* Inline media previews are enabled by default, but can be disabled on a per-account basis. This feature should be disabled if you have extreme privacy concerns or do not trust your contacts. This setting is always disabled for Tor accounts.
* **Known bug** related to adding friends and setting up the first OMEMO session. These will be addressed in a future release.

##### References

1. https://xmpp.org/extensions/xep-0363.html
2. https://github.com/iNPUTmice/ImageDownloader
3. https://modules.prosody.im/mod_http_upload.html
4. https://docs.ejabberd.im/admin/configuration/#mod-http-upload
5. https://xmpp.org/extensions/xep-0352.html

Changelog: https://github.com/chatsecure/chatsecure-ios/compare/v4.0.9...v4.1.0