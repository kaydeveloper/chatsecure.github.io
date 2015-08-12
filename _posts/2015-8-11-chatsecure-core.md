---
layout: post

title: ChatSecure Core
category: blog

author:
  name: Chris Ballinger
  twitter: chrisballingr
  gplus: 110173710196322914492 
  bio: Lead Developer
---

# ChatSecure Core

#### Motivation

I've noticed that many apps have been appropriating [ChatSecure iOS](https://github.com/chatsecure/chatsecure-ios) code for their whitelabeled products, even though the code is not currently suitable for this purpose. There are a lot of cross-dependencies, assumptions about the ChatSecure brand, and some unfortunate spaghetti code that has accumulated over the last few years of development. The GPL license also currently prevents people from legally shipping forks or devirative works that include our code to the App Store (without an exemption). Although many people and organizations have requested license exemptions since our move to the GPL, we haven't had the time or legal resources to grant any.

Now that we are also working on a whitelabeled version of ChatSecure ourselves, the pain of keeping the two versions in sync has made it apparent that a major refactor needs to happen as soon as possible. This will be done in two phases:

1. Creating a monolithic framework containing almost all of the existing ChatSecure iOS code.
2. Splitting that framework into multiple sub-frameworks each concerned with a single domain: UI, network, database, encryption. 

#### New License

Additionally, to accomodate forks and other open source projects that wish to reuse our code, we will be relicensing these reusable components under the copyleft [MPL 2.0](https://www.mozilla.org/MPL/2.0/) license. This is the license used by Firefox and [VLC for iOS](http://www.videolan.org/vlc/download-ios.html). It is most similar to the LGPL in that binary distributions require attribution and that modifications to the code need to be publicly available. It doesn't virally spread its terms to the rest of your program like the GPL, there's no issue with static linking like the LGPL, and it is fully compatible with the App Store.

Organizations that wish to release closed source / commerical / proprietary apps will also be able to use the code as long as they follow the terms of the MPL 2.0. In short, just give us proper attribution, and publicly distribute any source code changes you've made to our framework. 

## Refactor


This will require a very large refactor of the existing ChatSecure code into reusable components. Right now there is a tight coupling (aka spaghetti code) between the UI, XMPP network stack, database, and encryption layer. Each of these components will need to be split into reusable components with no cross-dependencies.

For the first step, we will create a monolithic ChatSecure framework that includes the entirety of the ChatSecure iOS code as a reusable library. This will allow improvements and security updates to the core ChatSecure code to be more readily available to whitelabeled apps.

After that is complete, we will begin splitting up the monolithic framework into smaller and more manageable frameworks: UI, network stack, database, and encryption layer. When that is complete, it will become much more feasible to create novel UI experiences that diverge from the upstream ChatSecure iOS UI code, without sacrificing the ability to easily merge in security updates and new backend features.

### Bonus: ChatSecure for Mac

As an unintended bonus of this work, it will then be possible to eventually create a native OS X desktop client for ChatSecure. The current standard for OTR+XMPP on OS X, [Adium](https://adium.im), hasn't been updated since last year but depends on Pidgin's libpurple, which is known for containing many [security holes](http://www.pidgin.im/news/security/). The lack of Adium updates puts users at risk, and it looks like new development is almost completely stalled. It also doesn't use OS X sandboxing so any Adium vulnerability allows an attacker to read and write (almost) any file on your computer, including past conversations, passwords, etc. We can fix that.

## On the Roadmap

#### Push

We are now well on our way to implementing our design for [decentralized push support](https://github.com/chatsecure/chatsecure-push-server), courtesy of a new grant from the [Open Technology Fund](https://www.opentechfund.org). Yes, we are finally fixing the [XMPP push problem](https://chatsecure.org/blog/fixing-the-xmpp-push-problem/)! We are very excited to ship beta versions of ChatSecure that will include this functionality in early Q4 2015. This is a feature that can be included in ANY app (we have SDKs for [iOS](https://github.com/chatsecure/chatsecure-push-ios) and [Android](https://github.com/chatsecure/chatsecure-push-android)), that allows your users to communicate with users of other apps. No more walled gardens!

This work is compatible with and compliments the existing effort to add [push support to XMPP](http://xmpp.org/extensions/xep-0357.html) itself.

#### Axolotl

We will also be integrating the mobile friendly Axolotl end-to-end encryption protocol into ChatSecure iOS, following the lead of the [Conversations team](http://conversationsgsoc2015.blogspot.de). This is the same protocol used by TextSecure/Signal, developed over at the amazing [Open Whisper Systems](https://whispersystems.org/blog/advanced-ratcheting/).

#### New Onboarding

We are also working on a streamlined onboarding process to help new users who are unfamiliar with the intricacies of XMPP. Stay tuned for more updates regarding that exciting new feature!

## A Bright Future for Secure Messaging

With all of these changes in place, we will be able to deliver a more seamless user experience that can rival that of other popular mobile messaging apps. We are committed to open source, open standards, decentralized protocols, and delivering the most secure and user-friendly product possible.

Thank you for your support!