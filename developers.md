---
layout: info
permalink: /developers/
title: Developers
---


## Source Code

The source code for all of our projects is hosted on GitHub.

* [iOS](https://github.com/chrisballinger/Off-the-Record-iOS) / [License](https://github.com/chrisballinger/Off-the-Record-iOS/blob/master/LICENSE) (GPLv3+) [[Contributing](https://github.com/chrisballinger/Off-the-Record-iOS/blob/master/CONTRIBUTING.md)]
* [Android](https://github.com/guardianproject/ChatSecureAndroid) / [License](https://github.com/guardianproject/ChatSecureAndroid/blob/master/LICENSE) (Apache 2.0)
* [chatsecure.org](https://github.com/chatsecure/chatsecure.github.io) (MIT / CC-BY-SA)

## Libraries

These free and open source libraries may be useful for other developers wishing to develop privacy-enhancing technologies. 

### OTRKit

[OTRKit](https://github.com/ChatSecure/OTRKit) is an Objective-C wrapper for the OTRv3 encrypted messaging protocol, using libotr. This library was designed for use with ChatSecure, but should theoretically work for Mac OS X as well with some minor tweaking to the build scripts.

[Source Code](https://github.com/ChatSecure/OTRKit)

### OnionKit

[OnionKit](https://github.com/chatsecure/onionkit) for iOS is still a work in progress. Eventually, it will be the basis of Tor support for ChatSecure on iOS in conjunction with [ProxyKit](https://github.com/chrisballinger/proxykit). You can track the progress of development on [GitHub](https://github.com/chatsecure/onionkit).

### More...

There are more open source security and privacy libraries available on [The Guardian Project Developers Page](https://guardianproject.info/code/).

## Build Instructions

### Website Build Instructions

[This website](https://github.com/ChatSecure/chatsecure.github.io) is rendered with [Jekyll](http://jekyllrb.com), a static website framework used by GitHub Pages.

    $ git clone git@github.com:ChatSecure/chatsecure.github.io.git
    $ cd chatsecure.github.io/
    $ jekyll build          # This will compile the website into _site/
    $ jekyll serve --watch  # This is very useful for development

### iOS Build Instructions

Clone the source code and required dependencies.

    $ git clone git@github.com:chrisballinger/Off-the-Record-iOS.git
    $ cd Off-the-Record-iOS/
    $ git submodule update --init --recursive

Install [mogenerator](http://rentzsch.github.io/mogenerator/). This keeps our Core Data models up to date. You'll need [Homebrew](http://brew.sh) first.

    $ brew install mogenerator
    
Create `/Off the Record/OTRSecrets.h` and fill in blank strings for the missing API keys:

* `USERVOICE_KEY`
* `USERVOICE_SECRET`
* `GOOGLE_APP_SECRET`
* `HOCKEY_LIVE_IDENTIFIER`
* `HOCKEY_BETA_IDENTIFIER`

Open `Off the Record.xcodeproj` in Xcode and build.


### Android Build Instructions

Clone the source code and required dependencies.

    $ git clone git@github.com:guardianproject/ChatSecureAndroid.git
    $ cd ChatSecureAndroid/
    $ git submodule update --init --recursive

Follow the [rest of the instructions here](https://github.com/guardianproject/ChatSecureAndroid/blob/master/BUILD).

