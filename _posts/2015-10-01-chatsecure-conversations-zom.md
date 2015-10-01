---
layout: post

title: ChatSecure, Conversations and Zom
category: blog

author:
  name: Chris Ballinger
  twitter: chrisballingr
  gplus: 110173710196322914492 
  bio: Founder & Lead Developer
---

# ChatSecure, Conversations and Zom

![ChatSecure, Conversations and Zom Logos](/images/chatsecure-conversations-zom.png)

We are excited to announce that major changes are planned for the underlying architecture of ChatSecure Android, and that there is a new UX-focused fork of the existing iOS and Android code bases called [Zom](http://zom.im). In the upcoming months, we will be releasing a new version of ChatSecure Android that will be powered by the core of [Conversations](http://conversations.im), as well as the first releases of Zom for iOS and Android. Both will have a new package name and signing key, so the [existing ChatSecure Android app](https://play.google.com/store/apps/details?id=info.guardianproject.otr.app.im&hl=en) will prompt you on every launch to either download the new version of ChatSecure or Zom.

## ChatSecure & Conversations

### Android

[Conversations](http://conversations.im) is currently (in my opinion) the best modern open source Android XMPP client. It was originally founded, and still primarily maintained, by [Daniel Gultsch](https://github.com/iNPUTmice). This summer he mentored [Andreas Straub's](https://github.com/strb) GSoC 2015 project to develop and implement a new XEP for asynchronous encryption based on Axolotl. They are calling it [OMEMO](http://conversations.im/omemo/) (OMEMO Multi-End Message and Object Encryption), and it's a genius way to adapt [TextSecure](https://whispersystems.org)'s fantastic [Axolotl](https://github.com/trevp/axolotl/wiki) protocol in a way that's compatible with almost every existing XMPP server (anything that supports [PEP](http://xmpp.org/extensions/xep-0163.html)).

The source code to the current version of [ChatSecure Android](https://github.com/guardianproject/chatsecureandroid) will soon be reaching end-of-life, and all new features and maintenance of that code will be happening in the [Zom Android](https://github.com/zom/zom-android) fork. The Zom fork is focused on a simplified and streamlined user experience, targeted toward a less tech-savvy crowd, and is primarily intended to compete with [WeChat](https://en.wikipedia.org/wiki/WeChat) in the Chinese and Tibetan markets.

To keep the ChatSecure™ brand consistent across platforms, we are partnering with Daniel Gultsch to create a whitelabeled version of Conversations to become the new ChatSecure Android. ChatSecure Android will continue to be offered for free on Google Play and [F-Droid](https://f-droid.org), but will be signed by a new key, so keep an eye out for that. We'll do our best to ease the transition.

Daniel and I discovered that we both have been working on methods to make it easier to whitelabel ChatSecure and Conversations. The primary purpose of these whitelabeling methods is to allow for downstream forks to more quickly and easily merge security updates and new features. As a nice side effect of this work, we will also soon be offering both automated and bespoke professional whitelabeling services to finally satisfy the (nearly constant) demand. 

*For more information about ChatSecure for Business, see below.*

### iOS

Soon we will be implementing [OMEMO Encryption](http://conversations.im/xeps/multi-end.html) in ChatSecure iOS, and immediately contributing our OMEMO XEP code upstream to [XMPPFramework](https://github.com/robbiehanson/XMPPFramework) so that other apps can benefit. We plan to utilize the pre-existing Objective-C library [AxolotlKit](https://github.com/WhisperSystems/AxolotlKit), written by [Frederic Jacobs](https://github.com/FredericJacobs), that has been used in production since the release of Open Whisper System's [Signal](https://itunes.apple.com/us/app/signal-private-messenger/id874139669?mt=8) v2.0 for iOS. Unfortunately AxolotlKit is still currently GPL (and therefore [not redistributable to the App Store](http://arstechnica.com/apple/2010/11/the-vlc-ios-license-dispute-and-how-it-could-spread-to-android/)) so this work is on hold until we can negotiate a change to an App Store-comptible copyleft license like [LGPLv2](http://www.gnu.org/licenses/old-licenses/lgpl-2.1.en.html) or [MPL 2.0](https://www.mozilla.org/en-US/MPL/2.0/) from [Fred](https://twitter.com/fredericjacobs) and [Moxie](Ohttps://twitter.com/moxie).

## ChatSecure & Zom

As I mentioned earlier, the [Zom fork](https://github.com/zom) is focused on a simplified and streamlined user experience, targeted toward a less tech-savvy crowd, and is primarily intended to compete with [WeChat](https://en.wikipedia.org/wiki/WeChat) in the Chinese and Tibetan markets.

### Android

[Zom Android](https://github.com/zom/zom-android) will have a radically different UI than the current version of ChatSecure Android, is a hard fork of the current code. Many advanced features will be hidden or removed for the sake of simplicity (with sane secure defaults of course!), which we feel is the right move when targeting the mass market. It will also only support a single account at a time, have a bigger focus on media sharing, and sport silly stuff like sticker packs.

Under the hood, it will still support OTR, XMPP, Tor, SQLCipher, certificate pinning, and all that crypto goodness that you expect, all bundled up behind a shiny new interface designed to hide or minimize the vast majority of the complexity. No use in having a secure messenger if it's as hard to setup and use securely as PGP, right?

### iOS

[Zom iOS](https://github.com/zom/Zom-iOS) is a soft fork of ChatSecure iOS, meaning it was designed to track upstream as closely as possible. We will continue to develop new features first in ChatSecure iOS, and push them to the downstream forks, such as Zom, as soon as they are stable. We will also ensure that security updates are available to every downstream fork as soon as possible.

Our [ChatSecure Core](https://chatsecure.org/blog/chatsecure-core/) whitelabeling system is made possible by the newly supported iOS 8.0+ dynamic frameworks. `ChatSecureCore.framework` contains the entirety of the upstream ChatSecure source code and resources, and allows for every string, image asset, and resource file to be customized via the [`OTRResources` bundle](Ohttps://github.com/zom/Zom-iOS/tree/master/Zom/OTRResources). 

Another nice bonus is that this work will open the door for ChatSecure for Mac, which will be the first open source, modern, native, sandboxed XMPP client for OS X. The lack of maintenance of [Adium](https://en.wikipedia.org/wiki/Adium) has made this issue especially urgent so, if you'd like to help, please be in contact!

## ChatSecure for Business™

Since early 2012 ChatSecure development has been financially supported by the following (outstanding) organizations: [The Guardian Project](https://guardianproject.info), [OpenITP](https://openitp.org), [Rights Action Lab](http://rightsactionlab.org), and the [Open Technology Fund](https://www.opentechfund.org). There have also been many smaller individual donations over the years (thank you)! Although open source grants and donations can be a great way to fund certain kinds of software development, the process can be glacial, arduous, and unforgiving at times. Even though I intend to continue funding ChatSecure development with grants for the immediate future, I still think it would be wise to begin diversifying our funding portfolio.

Despite living in Berkeley, with a close physical and social proximity to the frothy tech scene of San Francisco and Silicon Valley, I still have no desire to seek VC funding for ChatSecure. I was part of the first class to the awesome [Matter startup accelerator](http://matter.vc) as a co-founder to [OpenWatch](https://web.archive.org/web/20140908092952/https://openwatch.net/), an anti-authoritarian citizen journalism app. That whole concept didn't really fly in the VC world, so eventually we pivoted our core technology to become [Kickflip.io](https://kickflip.io), an open source mobile live broadcasting SDK + SaaS platform. My experience with the VC scene, although mostly pleasant, has made it very clear that traditional VC is a tough fit for open source privacy / security software.

### Whitelabel ChatSecure iOS and Android apps

I get emailed approximately once a week from some organization or individual who is seeking to produce a whitelabeled version of ChatSecure. In the past we haven't really had the resources to help to anyone, and even had to tell people to abandon their efforts due to the legal complexity of offering GPL license exemptions for the iOS client.

This has been the equivalent of leaving money on the table for years, especially considering I know for a fact there at least a few "illegal" forks of ChatSecure on the iOS App Store. I believe that ChatSecure should remain under a copyleft license for the benefit of the public good, but I never intended to prevent the free binary redistribution of our code on the App Store (an unfortunate side effect of the GPL) as long as the source code to your modifications remains available.

As I mentioned in a [previous blog post](https://chatsecure.org/blog/chatsecure-core/), future releases of ChatSecure iOS will be available under the [MPL 2.0](https://www.mozilla.org/en-US/MPL/2.0/), which is a fully App Store-compatible copyleft license (also used by Firefox and [VLC for iOS](http://www.videolan.org/vlc/download-ios.html)). It's most similar to the LGPL, so you only have to distribute the source to modified ChatSecure files, and you only have to seek a license exemption if you plan to modify upstream code.

This solution has extra benefits because it encourages downstream forks to minimize their modifications to upstream code, allowing them to more easily pull in security updates and new features. Most students, individuals, and small organizations won't need to pay for a license if they follow the requirements of the MPL.

Larger organizations and customers seeking bespoke solutions will desire the freedom to release deeper proprietary modifications, so we will be developing a fair pricing model to support these kinds of applications as well. This new revenue model can also help offset our reliance on grants, and allows for a greater diveristy of messaging products all built upon a solid ChatSecure foundation.

### ChatSecure SaaS

An XMPP client without a server is rather useless, so we will also be offering paid XMPP server and [ChatSecure Push](https://github.com/ChatSecure/ChatSecure-Push-Server) hosting. Since we believe in the power of open source software, both the client and server implementations will be completely free (as in source), and designed to be easily deployed by a moderately technical end user. Running your own secure XMPP server continues to be extremely difficult for the average person, so we intend to solve that:

1. **Paid SaaS hosting** for XMPP and Push infrastructure.
2. **Secure Server Hardware** solution for Enterprise networks that lives behind your corporate firewall.
3. **[HIPAA](https://en.wikipedia.org/wiki/Health_Insurance_Portability_and_Accountability_Act#HITECH_Act:_Privacy_Requirements)** and other data security regulation compliance.
3. **ChatSecure Server for Android**. Quick to setup, easily provision new devices, secure by default (end-to-end and at-rest), and user friendly.. even for novices! This open source Android XMPP server app will be based on [Prosody](https://prosody.im) and will use [Orbot's](https://www.torproject.org/docs/android.html.en) `.onion` services to provide universal [NAT traversal](https://en.wikipedia.org/wiki/NAT_traversal) (even over cell networks).

If you're interested in *ChatSecure for Business* please [send me an email](mailto:chris@chatsecure.org?subject=ChatSecure%20For%20Business) as soon as possible so we shape our product offerings to better match your needs in the upcoming months.

## Roadmap

### Push

We're on track to release the first beta version of ChatSecure Push in both Zom for iOS and Android, as well as ChatSecure for iOS. We'll be using separate federated instances to demonstrate decentralized push between multiple native mobile applications. We plan on integrating some components of ChatSecure Push into Conversations as well. It's by far the #1 most requested iOS feature, so I hope you'll like it.

### Axolotl / OMEMO

Work on implementing Axolotl / OMEMO into ChatSecure iOS will begin as soon as we can negotiate a license change to AxolotlKit. Hopefully we can sort that out quickly and get to work.

### Group Chat

We plan to support unencrypted group chat in ChatSecure iOS v3.2 this fall. Work on [np1sec](https://github.com/equalitie/np1sec) (aka [mpOTR](https://github.com/cryptocat/cryptocat/wiki/mpOTR-Project-Plan)) for multi-party OTR has been slow, but appears to be progressing. OMEMO works for small group chats as well, so we may adopt that in the meantime.

### ChatSecure for Mac

The ongoing `ChatSecureCore.framework` effort will soon make it possible to create a sandboxed desktop version of ChatSecure for Mac. Want to help? [Drop me a line.](mailto:chris@chatsecure.org?subject=ChatSecure%20For%20Mac)

### ChatSecure Server for Android

It's still too hard to host your own secure XMPP server. We are going to change that... some time next year.

### Business

We will be putting more effort toward providing secure communications tools to individuals, small teams, and larger businesses alike. Feel free to [reach out](mailto:chris@chatsecure.org?subject=ChatSecure%20for%20Business) if you'd like to discuss business applications for ChatSecure or have ideas about opportunities for growth.

### iOS 9 Tor VPN

As a quick side note, iOS 9 added a neat new API for full device VPN, which opens the door for a better way to implement Tor on iOS. [We are working on it!](https://github.com/icepa)

### Keybase Integration?

I had sort of a wild idea the other day to integrate ChatSecure with the [Keybase](https://keybase.io) API, which is basically a cryptographic identity provider and aggregator of your semi-decentralized signatures scattered around on Twitter, GitHub, etc. You can think of it as a successful mashup of a social network and a GPG keyserver. There's a lot of cool UX stuff we could do there, so I'd [like to hear](mailto:chris@chatsecure.org?subject=ChatSecure%20+%20Keybase) any ideas! Also, [Chris](https://keybase.io/chris), we should chat!

### Jobs

We will soon be hiring mobile, frontend, and backend developers with some or all of the following qualifications. 

* **iOS**: Objective-C, Swift, C, AutoLayout, Storyboards, CocoaPods, iPad, Cocoa, Mac UI, XCTest, an app in the App Store
* **Android**: Android 4.0 SDK and higher, Android NDK, Java, C, Android Studio, Gradle, JUnit, an app in the Play Store
* **Frontend**: HTML5, CSS, JavaScript, Bootstrap, Jekyll, Angular, React, Ember, your own website
* **Backend**: Python, Django, Ubuntu, Go, Rust, Docker, your own API
* **General Programming**: data structures, flow control, POSIX, standard stuff. Experience with Test Driven Development would be nice.
* **Security**: Some basic knowledge of cryptography is a must, but don't stress about the advanced stuff. You must have experience with modern secure / defensive coding practices, familiar with common vulnerabilites in native code, identifying potential areas of concern, surface area analysis, etc.
* **Open Source** contributions are highly recommended: individual projects, larger projects, pull requests, bug reports, QA, documentation, modular coding practices, semantic versioning, Travis-CI, GitHub, git. Know how to find the best existing open source libraries that solve a need. Be able to quickly assess a library's code quality and general maintenance health compared to similar projects. Know when to just rewrite it from scratch instead. Know how to properly publish your new open source library.
* **Freelance Contrators Only:** Sorry, there are currently no full time or permanent positions. Interns are OK though! If you're looking for that steady 9-5 you really should be looking somewhere else, because this ain't it. Fortunately Obamacare has made buying individual health insurance a lot better for us freelancers.
* **Equal Opportunity**: We do not discriminate based on race, color, sex, religion, national origin, age, disability, sexual orientation, genetic information, reprisal, socioeconomic class, radical political beliefs, tattoos, hair color, clothing style, or otherwise.
* **Berkeley, CA**: East Bay or SF preferred. Remote may be negotiable though!

Want to stand out by sending your application early? [Email me](mailto:chris@chatsecure.org?subject=ChatSecure%20Jobs) with a link to your GitHub profile and a short introduction.

### That's All Folks

Until next time. Thank you!