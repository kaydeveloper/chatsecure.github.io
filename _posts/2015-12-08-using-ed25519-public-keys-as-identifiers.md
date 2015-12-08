---
layout: post

title: Better XMPP Identifiers - Ed25519 Public Keys and .onions
category: blog

author:
  name: Chris Ballinger
  twitter: chrisballingr
  gplus: 110173710196322914492 
  bio: Founder & Lead Developer
---

# Better XMPP Identifiers - Ed25519 Public Keys and .onions

In a future version of ChatSecure I'd like to introduce a human-usable implementation of using entire public keys as identifiers. We are already experimenting with appending a portion of your [OTR](https://en.wikipedia.org/wiki/Off-the-Record_Messaging) fingerprint to your [XMPP](https://en.wikipedia.org/wiki/XMPP) username, but I'd like to take it a step further using some of the latest advances in [ECC](https://en.wikipedia.org/wiki/Elliptic_curve_cryptography).

### The Current State of XMPP Identifiers

Right now identifiers for XMPP-based apps ([`JID`](http://xmpp.org/extensions/xep-0029.html)) are currently in the form:

    username@domain.com
    
Where whichever person who first registered `username` on `domain.com` owns that identifier, similar to an email address. Even this basic level of complexity can be confounding for most non-technical people I've come across, so we've been doing what we can in our UX to relieve this complexity.

One of the main ways we've been simplifying things has been to implement QR-code and URL-based invite links of the form:

    https://chatsecure.org/i/#<base64 encoded JID + OTR fingerprint>
    
Which shows invited contacts links to download the apps if they don't have them, or directly opens ChatSecure to the add contact screen (with a somewhat-verified OTR key!).

### Ed25519 Public Key Cryptography
    
The great thing about [Ed25519](https://en.wikipedia.org/wiki/EdDSA) signing keys, is that that the whole public key can fit into 32-bytes. That's equivalent to 32 ASCII characters (between 0-255). To allow for a more seamless representation (non-alphanumeric ASCII characters can be a bummer), you can use hex, for example:

    7388a1238a0865a74d721861356d3f7869c598494ff906a52e15338585a02c00
    
This is 32-bytes of random data from [`random.org`](https://www.random.org), which in theory could represent an entire Ed25519 public key. Using other encodings such as [Base64](https://en.wikipedia.org/wiki/Base64) can result in an event shorter output:

    c4ihI4oIZadNchhhNW0/eGnFmElP+QalLhUzhYWgLAA
    
But unfortunately XMPP JIDs don't play well with Base64 because JIDs are case-insensitive. We can, however, use [Base32](https://en.wikipedia.org/wiki/Base32) to shrink the size while still maintaining compatibility with XMPP JIDs:
    
    ooekci4kbbs2otlsdbqtk3j7pbu4lgcjj74qnjjocuzylbnafqaa
    
Now that we have our username portion, let's solve the other big problem with XMPP JIDs... the server.

### Let's Get Rid of XMPP Servers

Although there are some trustworthy XMPP servers out there, you can never be more secure than hosting your server yourself on hardware you own. Traditionally this has been a problem for non-technical users. Asking them to SSH into their headless Raspberry Pi to `apt-get install prosody` won't get you the results you'd want.

For technical users, on the other hand, one of the main problems has often been the lack of a [publicly reachable](https://en.wikipedia.org/wiki/IP_address#Public_addresses) IP address. Fortunately by utilizing Tor [`.onion`](https://en.wikipedia.org/wiki/.onion) services, you can have a reachable address from *anywhere*, even behind carrier-grade NAT (like on a cellphone)!

`.onion` addresses are an 80-bit number represented in base32 and look like this:

    wlcpmruglhxp6quz.onion
    
The above example is the `dukgo.com` XMPP server's `.onion` address.

### Similar Work

A similar approach to the `.onion` endpoints has been taken by the [Ricochet](https://en.wikipedia.org/wiki/Ricochet_(software)) project.

They replace both the username and server with the `.onion` address itself. The main drawback (or feature, depending on your viewpoint) is that it's a ground-up rewrite of a full stack chat client, which means no interoperability for existing XMPP clients.

[Pond](https://pond.imperialviolet.org) also operates in a similar way as far as `.onion` addresses, but as far as I know there's still only a rudimentary GUI and command line client, which limits its usefulness to very technical users.

My approach would be completely backwards compatible with existing XMPP clients, where you could use the same Ed25519 identifier on multiple servers (including your own `.onion`) to ensure reachability by all of your contacts, regardless of their client of choice.

### A Glorious Dawn

Using this new public key identifier, you can sign your other cryptographic identities and identifiers, and upload the results to [`keybase.io`](https://keybase.io), or wherever. New contacts can automatically verify your identity, and can use our new QR-code invites and links to avoid typing these long strings.

    ooekci4kbbs2otlsdbqtk3j7pbu4lgcjj74qnjjocuzylbnafqaa@wlcpmruglhxp6quz.onion
    
This above example could be your fully valid JID containing your public key and personal `.onion` address. Because no human would ever type that in, we can share it in link form:

* [Invite Link URL](https://chatsecure.org/i/#b29la2NpNGtiYnMyb3Rsc2RicXRrM2o3cGJ1NGxnY2pqNzRxbmpqb2N1enlsYm5hZnFhYUB3bGNwbXJ1Z2xoeHA2cXV6Lm9uaW9u) (Link will 404, server/client support still in progress)
* [XMPP URI](ooekci4kbbs2otlsdbqtk3j7pbu4lgcjj74qnjjocuzylbnafqaa@wlcpmruglhxp6quz.onion)
* QR Code ![QR Code Example](/images/invite_qrcode_sample.jpg)

You can still have a human-readable username in your [XMPP vCard](http://xmpp.org/extensions/xep-0054.html), so you can choose whatever 'username' you'd like without creating a collision. You can also upload signatures of your [OTR](https://en.wikipedia.org/wiki/Off-the-Record_Messaging), [PGP](https://en.wikipedia.org/wiki/Pretty_Good_Privacy#Design), or [Axolotl](https://github.com/WhisperSystems/Signal-Android/wiki/ProtocolV2) identities (using this same Ed25519 key) to your vCard to help contacts auto-verify your cryptographic identity.

### Contrived Example

Bob serendipitously meets Alice in a crowded bar and they instantly hit it off by talking about obscure cryptographic protocols. A loud band starts playing and they have difficulty maintaining conversation, so they decide to move their communication to a secure channel.
 
Bob opens up the latest version of ChatSecure, and tries to share his Invite URL to Alice's phone via a secure [Bluetooth LE](https://en.wikipedia.org/wiki/Bluetooth_low_energy) channel. Due to the crowding of the 2.4 GHz channel, they have trouble establishing a connection, and decide to switch to QR codes, which should work well in the dim lighting.

Alice successfully scans Bob's QR code Invite URL, which opens up her browser to `chatsecure.org/i/#...`, where she sees how to download the latest version of ChatSecure. Once the app finishes downloading, she clicks the same link again, but this time instead of opening her browser, it opens ChatSecure to the Add Contact screen. Bob's account details are shown on the screen, and she can see his other cryptographic identities being pulled down in realtime from Keybase.

Now that they have established a secure channel, they decide that this music is too loud anyway, and it would be a good point to leave the bar and drink some coffee at one of their apartments. An encryption success story!

### Roadmap

This is just one of many exciting changes I want to bring in the months ahead. Coming very soon will be a new iOS release with group chat, slick onboarding, and... **push notifications**. 🚀

Stay tuned!