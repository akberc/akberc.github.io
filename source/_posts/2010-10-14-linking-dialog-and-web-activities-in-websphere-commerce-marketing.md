---
layout: post
title: Linking Dialog and Web Activities in WebSphere Commerce Marketing
tagline: out-of-the-box features
date: 2010-10-14 23:10:00+00:00
tags: [ibm, websphere, commerce, marketing]
category: ecommerce
comments: false
---
IBM WebSphere Commerce 7.0 comes with a substantial set of marketing activities, namely web activities, e-mail activities and dialog activities.  These are all part of a feature known as 'Precision Marketing' which works roughly as follows: 

An active customer action or a background processing action causes a 'trigger' to fire.  If this triggering can be scoped to a 'target' (qualification), then an 'action' occurs.  

Activity types: Web and e-mail activities push content along, while dialog activities respond to specific shopper request behaviour.

**Poor Man's Recommendation Engine:** Now, a recommendation engine pushes content and products based on past shopper behaviour, whether specific to that shopper, or general past shopper behaviour.

If a dialog activity's end action is to persist captured user behaviour, then triggers and targets based on the persisted behaviour can then be used in a web activity to display specific content.

Thus, combining the two with some custom enhancements that put together some logic and data storage and you may have a specialised recommendation engine for your specific business needs.
