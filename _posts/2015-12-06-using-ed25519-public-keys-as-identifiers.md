---
layout: post

title: Better XMPP Identifiers: Ed25519 Public Keys and .onions
category: blog

author:
  name: Chris Ballinger
  twitter: chrisballingr
  gplus: 110173710196322914492 
  bio: Founder & Lead Developer
---

# Better XMPP Identifiers: Ed25519 Public Keys and .onions

In a future version of ChatSecure I'd like to introduce a human-usable implementation of using entire public keys as identifiers. We are already experimenting with appending a portion of your OTR fingerprint to your XMPP username, but I'd like to take it a step further using some of the latest advances in ECC (Eliptic Curve Cryptography).

### The Current State of XMPP Identifiers

Right now identifiers for XMPP-based apps (`JID`) are currently in the form:

    username@domain.com
    
Where whichever person who first registered `username` on `domain.com` owns that identifier, similar to an email address. Even this basic level of complexity can be confounding for most 'normal' people I've come across, so we've been doing what we can in our UX to relieve this complexity.

One of the main ways we've been simplifying things has been to implement QR-code and URL-based invite links of the form:

    https://chatsecure.org/i/#<base64 encoded JID + OTR fingerprint>
    
Which shows invited contacts links to download the apps if they don't have them, or directly opens ChatSecure to the add contact screen (with a somewhat-verified OTR key!).

### Ed25519 Public Key Cryptography
    
The great thing about Ed25519 signing keys, is that that the whole public key can fit into 32-bytes. That's equivalent to 32 ASCII characters (between 0-255). To allow for a more seamless representation (non-alphanumeric ASCII characters are a bummer), you can use hex, for example:

    7388a1238a0865a74d721861356d3f7869c598494ff906a52e15338585a02c00
    
This is 32-bytes of random data from `random.org`, which in theory could represent an entire Ed25519 public key. Using other encodings such as base64 can result in an event shorter output:

    c4ihI4oIZadNchhhNW0/eGnFmElP+QalLhUzhYWgLAA
    
But unfortunately XMPP JIDs don't play well with base64. We can, however, use base32 to shrink the size while still maintaining compatibility with XMPP JIDs:
    
    ooekci4kbbs2otlsdbqtk3j7pbu4lgcjj74qnjjocuzylbnafqaa
    
Now that we have our username portion, let's solve the other big problem with XMPP JIDs... the server.

### Let's Get Rid of XMPP Servers

Although there are some trustworthy XMPP servers out there, you can never be more secure than hosting your server yourself on hardware you own. Traditionally this has been a problem for non-technical users. Asking them to SSH into their headless Raspberry Pi to `apt-get install prosody` won't get you the results you'd want.

For technical users, on the other hand, one of the main problems has often been the lack of a publicly reachable IP address. Fortunately by utilizing Tor `.onion` services, you can have a reachable address from *anywhere*, even behind carrier-grade NAT (like on a cellphone)!

`.onion` addresses are an 80-bit number represented in base32 and look like this:

    wlcpmruglhxp6quz.onion
    
The above example is the `dukgo.com` XMPP server's `.onion` address.

### A Glorious Dawn

Using this new public key identifier, you can sign your other cryptographic identitites and identifiers, and upload the results to `keybase.io`, or wherever. New contacts can automatically verify your identity, and can use our new QR-code invites and links to avoid typing these long strings intended for the computer.

    ooekci4kbbs2otlsdbqtk3j7pbu4lgcjj74qnjjocuzylbnafqaa@wlcpmruglhxp6quz.onion
    
This above example could be your fully valid JID containing your public key and personal `.onion` address. Because no human would ever type that in, we can share it in link form:

* URL: [https://chatsecure.org/i/#b29la2NpNGtiYnMyb3Rsc2RicXRrM2o3cGJ1NGxnY2pqNzRxbmpqb2N1enlsYm5hZnFhYUB3bGNwbXJ1Z2xoeHA2cXV6Lm9uaW9u](https://chatsecure.org/i/#b29la2NpNGtiYnMyb3Rsc2RicXRrM2o3cGJ1NGxnY2pqNzRxbmpqb2N1enlsYm5hZnFhYUB3bGNwbXJ1Z2xoeHA2cXV6Lm9uaW9u)
* XMPP URI: [xmpp:ooekci4kbbs2otlsdbqtk3j7pbu4lgcjj74qnjjocuzylbnafqaa@wlcpmruglhxp6quz.onion](ooekci4kbbs2otlsdbqtk3j7pbu4lgcjj74qnjjocuzylbnafqaa@wlcpmruglhxp6quz.onion)

You can still have a human-readable username in your XMPP vCard, so you can choose whatever 'username' you'd like without creating a collision.

This is just one of many exciting changes I want to finish in the months ahead. Coming very soon will be a new iOS release with group chat, onboarding, and... **push notifications**. 🚀

Cheers!