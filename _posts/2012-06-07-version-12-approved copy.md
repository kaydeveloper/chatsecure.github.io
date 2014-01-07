---
layout: post

title: Version 1.2 Approved
category: blog

author:
  name: Chris Ballinger
  twitter: chrisballingr
  gplus: 110173710196322914492 
  bio: Lead Developer
---

[![guardian project logo](/images/guardian_banner.png)](https://guardianproject.info/)

I would like to announce a partnership with [The Guardian Project](https://guardianproject.info/), who develops the Android equivalent of ChatSecure called [Gibberbot](https://guardianproject.info/apps/gibber/), along with a whole suite of mobile security applications. It's an exciting time for open-source secure mobile communications!

Version 1.2 has been approved! This new version includes support for limited **background messaging**, the #1 most requested feature. Yay!

### Background Messaging

Unfortunately, Apple's policies prevent the creation of secure chat applications that run in the background indefinitely. The only way to get backgrounded sockets on iOS is to register your app as "VoIP", but unless you actually implement VoIP services, you will get rejected from the App Store. A common workaround used by other chat programs is to run the real chat client server-side and run a "push service" that sends the messages to your phone. That approach is unacceptable for this app because it would require me to build my own push server, which comes with quite a few drawbacks:

*   Centralized storage of login credentials
*   Single point of failure
*   Vulnerable to eavesdropping
*   Expensive to build and maintain
*   [Maximum size allowed for a notification payload is 256 bytes](http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html), and is "best effort" and not guaranteed.

The only other option is to 'trick' the OS into continuing to run the application in the background by starting a "long running task" during the `applicationDidEnterBackground:` in your app delegate, which in this case is an `NSTimer` set to fire every 10 seconds or so. The main limitation to this approach is that unless you manually restart the app every 10 minutes, it will be force-closed by the OS. This is similar to the technique used by the awesome [Verbs](http://verbs.im/) app, who graciously helped me tackle this problem.