---
layout: post
title: "Automatic, Site-Agnostic, Unified Delivery Tracking"
permalink: /stack-hacking
---

### Outline

1. Deliveries
  - Cross-platform (OSX, iOS.  ??: Windows, Linux, Android)
  - Gives specific locations
  - Adds calendar events to indicate when deliveries will occur, including
    a checkmark indicating completion.
2. Junecloud
  - Better than iCloud syncing because they handle automatically tracking
    shipments, rather than having to add them manually. Still
    cross-platform, as expected.
    - Their parsing methods: Specific integrations for lots of
      distributors, including Amazon (link to Deliveries' docs for this).
      Otherwise just attempt to parse a tracking number when available.
      You can send an entire email with lots of extraneous text, they'll
      just parse the relevant number.
3. Automatic mail-forwarding with Gmail (should work for any other service)
  - Caveat: You're automatically sending emails to a third-party, which
    might have security implications. As long as you've got
    decent/accurate filters that catch only shipping emails, I think
    you're fine.
  - Catch any mail with trigger words: 'shipping', 'tracking', etc (see filter)
  - Automatically send Amazon confirmations to track@junecloud.com
