---
layout: post

title: ChatSecure v1.3 Progress
category: blog

author:
  name: Chris Ballinger
  twitter: chrisballingr
  gplus: 110173710196322914492 
  bio: Lead Developer
---

I have been mainly working on UI / usability improvements and trying to iron out some persistent bugs. Here are the things that still need to be done before the 1.3 release:

*   Figure out how to properly downgrade conversation to plaintext (Ian's explanation on the otr-dev mailing list wasn't clear to me, so maybe Miron could be of help)
*   Hopefully this will fix the "missing messages" bug.
*   Rigorously test the security of the new password storage mechanism (uses iOS keychain)
*   Make the XMPP SSL certificate-checking options (hostname mismatch, or allowing self-signing) per-account, rather than global, and only for custom XMPP accounts.
*   Implement SSL cert verification if possible.
*   Fix the "multiple conversations with the same buddy" bug.