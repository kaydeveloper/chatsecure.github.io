---
layout: post

title: Fixing the XMPP Push Problem
category: blog

author:
  name: Chris Ballinger
  twitter: chrisballingr
  gplus: 110173710196322914492 
  bio: Lead Developer
---

## Fixing the XMPP Push Problem

XMPP is at serious risk of being permanently replaced by proprietary alternatives that have already solved the mobile push messaging problem. Remember in the 90s how many closed IM networks there were? Today it is much worse.

## Current Approaches

### Thin Client

Run a thin XMPP client on a 'man-in-the-middle' server that can relay messages to clients via push message when mobile clients aren't actively connected. Many iOS messenger apps use this method without clearly informing the user.

Pros:

* Can add push support for any arbitrary XMPP server

Cons:

* Very obvious, centralized point of failure
* Allows for easy eavesdropping or even active MITM attacks
* Requires plaintext storage of remote login credentials (e.g. Gmail passwords)

Examples:

* [Verbs Pro](http://verbs.im) (iOS)
* [IM+](https://plus.im) (iOS, Android, Web)



### Persistent Socket

Persistent sockets is how XMPP was originally designed to work. Acquire a long-lived socket and keep it open... forever. Android apps are able to use this method, as well as iOS apps that declare VoIP functionality. On iOS this socket is supposed to be for VoIP signaling only, so you can be terminated by the OS for too much activity while in the background (e.g. presence updates).

Pros:

* XMPP works as designed, most of the time
* No modification to existing infrastructure

Cons:

* Battery drain because the antenna cannot be powered down
* Disconnection can still occur from wireless network problems
* iOS apps can still be terminated by the OS under memory pressure or too much socket activity

Examples:

* [ChatSecure](https://chatsecure.org) (Android version only)
* [Monal](http://monal.im) (iOS)

### Abandon XMPP Compatibility

Many apps have abandoned traditional XMPP in favor of proprietary modifications that lack federation and interoperability. WhatsApp took [ejabberd](http://www.ejabberd.im), an open source XMPP server written in Erlang, and modified it to send native push messages, but of course it only works with their official apps.

Pros:

* Relatively easy to implement
* Lock in users to your proprietary ecosystem

Cons:

* Locks you in to their proprietary ecosystem
* No federation between domains
* No federation between apps: each app developer taking this approach is their own silo, unable to communicate with any others

Examples:

* [WhatsApp](http://www.whatsapp.com)
* [TextSecure](http://en.wikipedia.org/wiki/TextSecure) (however, email identifiers and a limited form of federation are coming soon)

## How Push Messages Work

If you're not familiar with Apple's [APNs](https://en.wikipedia.org/wiki/Apple_Push_Notification_Service) or Google's [GCM](https://en.wikipedia.org/wiki/Google_Cloud_Messaging), these services are the officially sanctioned way of sending push messages to mobile apps. However, there are certain limitations that prevent easy XMPP-style federation:

* You cannot (easily) send push messages to someone else's app
* Push messages on iOS are not guaranteed to be delivered (although they usually are)
* Push message payloads on iOS cannot be processed by the app in the background before iOS 7

The biggest problem is that there is no easy way to send push messages between my app and your app. For me to send a push to one of your app's users on iOS, I must first obtain an APNs SSL certificate/key pair from you, and one of your user's 'push token' that uniquely identifies their device to Apple. These push tokens are potentially sensitive information because they allow Apple to locate your device (in order to send it a push).

## Solving Inter-app Push

To solve the XMPP push problem, we need multiple pieces of new infrastructure:

1. Solve the problem of how to send raw push messages between two arbitrary apps.
2. Define spec for where clients (apps) should send messages when contact is "offline"
3. Define spec for where servers should send messages when contact is "offline" 

Instead of having each app developer manually provide every other app developer an SSL push certificate and push tokens, an intermediary server can be built to automate this process and obscure the actual push tokens, as well as control potential spam.

However, this approach will require cooperation between XMPP clients and XMPP servers in order for federation to work properly.

ChatSecure iOS can connect to almost any XMPP server, so it can be a client for multiple JIDs. A user could have the accounts "alice@example.com" and "alice@jabber.org" and expect to receive background notifications for both accounts. This means the operators of the XMPP servers for example.com and jabber.org will need to understand and implement our spec to send pushes to our client.

### Push Relay Server

This is the server that sends the final push to the app user. It will need to accept POSTs from authorized pushers, which can include XMPP server operators, individual app developers with other relay servers, or even other end users. For ChatSecure iOS we can do this by having users register a unique username/password with our instance of the push relay server, tied to an optional email address identifier for password resets. 

After registering a "ChatSecure Push" account, you must add a device to receive pushes, which includes the required information for delivering the final push message (the APNs token) and probably a user friendly identifier / basic device info.

To receive push messages to your account (which are then forwarded to all your registered devices), you must request a whitelist token from the server to give to your friends and authorized XMPP servers. Anyone with a whitelist token will be able to send you messages directly to all of your devices by crafting a POST message to our relay server.

An old draft of how this server might work is [available here](https://github.com/ChatSecure/ChatSecure-Push-Server/blob/master/docs/v3/README.md) but it needs to be updated because we identified serious problems with this spec a long time ago. However, we never updated the draft online from our notes, so we lost all of that work. Great.

### XMPP Clients

XMPP clients will need a way to ask another clients if they support receiving pushes via a relay. Since pushes can be sent from anywhere, clients will also be able to send pushes directly to other clients through the relay as long as they have their friend's whitelist token. They will also need to respond to XMPP server inquiries for whitelist tokens to allow pushes to be sent by the server if a message is sent by a client not supporting direct push.

### XMPP Servers

XMPP servers can ask their connected clients if they support push relays and, if so, forward messages they receive to the push relay server when the client is offline. This will require the XMPP server to obtain a whitelist token from the user as well.

### Non-XMPP Clients

Because this method can bypass the XMPP server entirely, it allows for non-XMPP protocols to participate.

## What Still Needs to be Done

We need to fix/finish our server [draft spec](https://github.com/ChatSecure/ChatSecure-Push-Server/blob/master/docs/v3/README.md) and deploy a proof of concept XMPP server and push relay for the chatsecure.org domain. Additional work will also need to be done to integrate this for the ChatSecure clients.

There are many issues to be overcome, and there are very few developers who care about developing an interoperable standard because there is absolutely no financial incentive... and it is very difficult to do correctly. Proprietary messaging apps can get hundreds of millions in financing and large teams of engineers. We have to make do with much, much less.

Another big problem is that OTR is incompatible with this approach unless we use hacks to wake up clients to establish new sessions but, even if we do that, the messages won't be able to be decrypted by multiple devices. The TextSecure protocol may provide some answers here, but they also haven't solved the inter-app federation problem in a way that allows users to run their own backend or custom TextSecure clients.

Perhaps work should be directed toward extending the TextSecure infrastructure to support inter-app communication and federation instead of extending the aging OTR and XMPP protocols beyond their meaningful lifetime.