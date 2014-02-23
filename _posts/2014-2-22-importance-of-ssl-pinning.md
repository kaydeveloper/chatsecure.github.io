---
layout: post

title: The Importance of SSL Pinning
category: blog

author:
  name: Chris Ballinger
  twitter: chrisballingr
  gplus: 110173710196322914492 
  bio: Lead Developer
---

![SSL Pinning Support](/images/ssl_pinning.jpg)

You may have noticed there was a [very important security update](http://support.apple.com/kb/HT6147?viewlocale=en_US&locale=en_US) for iOS devices lately that patches a flaw allowing the complete bypass of certificate checks for any apps that use the default system-wide TLS library, Security.framework. There is a pretty good description of the vulnerability [here](https://www.imperialviolet.org/2014/02/22/applebug.html), if you're interested.

If you use the latest versions of ChatSecure you are now using a feature called SSL pinning that allows for you to manually inspect and remember the SSL certificates of the servers you connect to, bypassing the CA system entirely. 

**However**, if you do not update to iOS 7.0.6 or higher and you are being actively [MitMed](https://en.wikipedia.org/wiki/Man-in-the-middle_attack), the alert dialog ([pictured above](/images/ssl_pinning.jpg)) may provide misleading information in the form of a green ✓ instead of a red ✗ with the appropriate certificate error. This is because XMPPFramework's socket library, GCDAsyncSocket, relies on Apple's faulty SSL verification routine. Fortunately the displayed SHA-1 hash will still not match, so it is especially important to check the double-check the fingerprint of any new certificate before you store it.

It is especially important to update all of your devices as soon as possible because apps that don't implement certificate pinning will not display any warning at all when your connection is compromised. Unfortunately most apps do not implement this functionality, [including many banking apps](http://blog.ioactive.com/2014/01/personal-banking-apps-leak-info-through.html).

Additionally, if you are using OS 10.9.1, please avoid using Safari (or other programs that use Security.framework) until this vulnerability is patched on OS X as well.