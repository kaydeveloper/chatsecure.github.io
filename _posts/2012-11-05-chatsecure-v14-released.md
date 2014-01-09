---
layout: post

title: ChatSecure v1.4 Released
category: blog

author:
  name: Chris Ballinger
  twitter: chrisballingr
  gplus: 110173710196322914492 
  bio: Lead Developer
---

In October we finished up v1.4 which includes XEP-0184 (delivery receipts), XEP-0085 (chat state) and a redesigned login screen. We have also been working on privacy-minded solutions to the lack of push messaging support (ChatSecure Push Server) as well as additional avenues for backgrounded sockets.

* XEP-0184: Delivery receipts. This feature is in Gibberbot as well, which allows for clients to be notified when their messages are received by the other chat participant.
* XEP-0085: Chat State. This feature allows users to see when other people are typing a message, and gives them the option to send those notifications as well.
* Redesigned login screen: Completely refactored the login screen to be more extensible in the future. We also added a port field for custom XMPP servers.
* <a href="https://github.com/ChatSecure/ChatSecure-Push-Server">ChatSecure Push Server</a>: A working proof-of-concept server has been built, and we are now working on client integration, as well as other options to allow for long running background sockets.

 [Free Download](http://itunes.apple.com/us/app/chatsecure/id464200063?mt=8) ([changelog](https://github.com/chrisballinger/Off-the-Record-iOS/compare/v1.3...v1.4))