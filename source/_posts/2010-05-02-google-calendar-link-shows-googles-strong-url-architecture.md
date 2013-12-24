---
author: akberc
comments: false
date: 2010-05-02 10:55:00+00:00
layout: post
slug: google-calendar-link-shows-googles-strong-url-architecture
title: Google Calendar Link shows Google's Strong URL architecture
wordpress_id: 15
categories:
- google
- server
tags:
- apps
- architecture
- calendar
- google
- url
---
Quick Post:  Just tried this today and it worked:

Travel and meeting sites can give you a link that can add an entry to your Google Calendar, among ICAL and other links thare are also provided.  This is very handy, as it takes care of time zones etc. and works out quite well.  The link is usually of the type:


> http://www.google.com/calendar/event?action=TEMPLATE&text=. . . . .


If you are on your company's Google Apps hosted calendar, this link would not work and it would ask you to log in to a regular google account, not a Google Apps for Business calendar.  If you copy the link location and add after 'calendar/':


> http://www.google.com/calendar/hosted/xxxx.com/event?action=TEMPLATE&text=. . . . .


where 'xxxx.com' is your Google Apps domain, it works like a charm. Kudos to Google URL architecture and those that enforce it.

