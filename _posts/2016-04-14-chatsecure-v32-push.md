---
layout: post

title: ChatSecure iOS v3.2 - Decentralized Interoperable Push Support
category: blog

author:
  name: Chris Ballinger
  twitter: chrisballingr
  gplus: 110173710196322914492 
  bio: Founder & Lead Developer
---

# ChatSecure iOS v3.2 - Decentralized Interoperable Push Support


With the release of [ChatSecure iOS v3.2](https://itunes.apple.com/us/app/chatsecure-encrypted-messenger/id464200063), we have enabled the first phase of a new form of push messaging that is decentralized, interoperable, and reduces identifiable metadata. Users of any app compatible with the [ChatSecure Push protocol](https://github.com/ChatSecure/ChatSecure-Push-Server/tree/master/docs/v3) can send push messages across app boundaries, starting with the latest release of ChatSecure iOS and the next version of [Zom Messenger](https://zom.im). These push messages currently contain no content and are simply a way to wake up the receiving client for ~20 seconds. 

Unlike centralized messaging applications like WhatsApp, Signal or Telegram, a core part of our mission is to allow users to connect any XMPP server of their choice and to encourge users to run their own servers. This privacy win also comes with a major drawback for iOS users, because Apple prevents the application from running in the background. The only way push messages can be sent are through servers run by app developers themselves, which presents a problem when trying to support push for any arbitrary XMPP server.

### Example Flow

Alice (`alice@example.com`) and Bob (`bob@example.com`) are both using the ChatSecure iOS app to communicate via their private XMPP server `example.com`. After each OTR session is established, they each send a payload inside the OTR channel that contains a fresh token and their push API endpoint. The token is used by the API endpoint to lookup your device APNS token, and the endpoint parameter is what allows this to work between apps from different developers. Because all of this data is exchanged by the clients themselves, our push server has no idea about the JIDs of Alice or Bob, or where any of the tokens ended up.

![Contact Offline](/images/contact-offline.png)

The next time Alice opens the app and she wants to talk to Bob, she sees that Bob is offline. 

![Knock Sent](/images/knock-sent.png)

On the chat screen there is now a new button called Knock that has replaced the Send button when the contact is offline (and no text is entered). By pressing Knock, it looks up the token and endpoint that Bob gave her earlier, and sends a HTTP POST to that endpoint with the token.

![Contact Online](/images/contact-online.png)

About 5 seconds later Bob's client will wake up in the background and automatically login to his XMPP account. 

![Knock Received](/images/knock-received.jpg)

His device will also receive back the token he gave to Alice, do a local lookup to see that the incoming push is coming from Alice, and show a local notification visibile on the lock screen. We are able to keep the app open for about 20 seconds in the background, which is enough time for Alice to establish a new OTR session and send a few messages.

### Improving the UX

Having a Knock button is not the ideal user experience because it's a foreign UI concept and not immediately clear how it works. Originally we tried to automatically trigger knock messages, but hit issues with missing messages caused by sending messages to offline contacts, or when in a stale OTR session. Our message pipeline needs to be reworked to handle these cases and ensure that no message ever enters a black hole.

There is a relatively new way for XMPP servers to interact with app push gateways called [XEP-0357](http://xmpp.org/extensions/xep-0357.html) but not very many servers support this extension right now. Our current solution works immediately with any XMPP server as long as you're both running a ChatSecure Push compatible client. In the future we will roll out client support for XEP-0357 to allow you to receive pushes from any contact, as long as you're connected to a compatible XMPP server.

### The Road Ahead

Although OTR has proven to be trustworthy over the years, it is showing its age in the face of more modern protocols like [SignalProtocol](https://whispersystems.org/blog/signal-inside-and-out/) (formerly known as Axolotl). Originally we wanted to integrate Axolotl/[OMEMO](https://conversations.im/omemo/) but we haven't been able to acquire a license from Open Whisper Systems. The next post will be about our plans, in collaboration with the Conversations team, to implement a revision of OMEMO that supports [Olm](https://matrix.org/git/olm/about/) instead of SignalProtocol. 