---
layout: post

title: v1.3 Status Update
category: blog

author:
  name: Chris Ballinger
  twitter: chrisballingr
  gplus: 110173710196322914492 
  bio: Lead Developer
---

A number of changes have been committed to the master branch since the last status update:

*   The refactoring required for multiple account support is almost complete.
*   Global XMPP SSL certificate verification preferences have been removed and have been replaced with per-account settings. (Thanks to Chris Gahan for mentioning it before it was ever a problem)
*   Currently there is no UI for relaxing the cert checks anymore, but the underlying code is in place. This will need to be hooked up toOTRLoginViewController and tested thoroughly before v1.3 submission.
*   Some UI elements have been simplified or merged into other views.
*   The Conversations view (only available on iPhone) has been eliminated and has been replaced by an editable "Recents" list at the top of your Buddy List on both iPhone and iPad.
*   Adding accounts is now done directly from the Settings screen.
*   Fixes have been made to the logic for when to show message notifications
*   It also doesn't crash anymore when trying to reply under certain scenarios
*   Support for sharing a link to the App via Twitter on iOS 5 and higher.

There are still some issues related to not properly downgrading back to plaintext aftercancelinga secure conversation that need to be fixed before the next update as well. Once that is figured out, we should be on track for submission to the App Store very soon!