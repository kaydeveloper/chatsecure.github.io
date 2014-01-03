---
layout: info
permalink: /faq/
title: Frequently Asked Questions
cover_image: blog-cover.jpg
---

## Q: Why can't ChatSecure for iPhone stay connected in the background?
The short answer is we can't stay connected or 'always on' because Apple doesn't let us.

There are a few cases in which an app can stay running in the background:

* ﻿Apps that play audible content to the user while in the background, such as a music player app
* Apps that keep users informed of their location at all times, such as a navigation app
* Apps that support Voice over Internet Protocol (VoIP)
* Newsstand apps that need to download and process new content
* Apps that receive regular updates from external accessories

iOS 7 only apps can be 'woken' to perform tasks:

* Background Fetch (timed based; not consistent; like newsstand behavior﻿)
* Remote notifications (we're looking into using this for a push service)
* Background downloads using NSURLSessionDownloadTask﻿ (not helpful for our needs)

We are not any of these therefore we are limited to about 10 minutes of background time. We support alerting you when there is only 1 minute left. At that point if you open ChatSecure again before the 10 minutes are up we are given another 10 minutes of background time once Chatsecure enters the background again.