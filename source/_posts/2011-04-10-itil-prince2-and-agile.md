---
layout: post
title: ITIL, PRINCE2 and Agile
tagline: back-of-envelope thoughts
date: 2011-04-10 23:10:00+00:00
tags: [itil, prince2, agile, project, programme]
category: management
comments: false
---
Enterprise systems required service management to ensure that newly deployed projects run in a predictable and manageable manner.  The discipline and project managment that enabled project delivery should continue in some form.  The project has now become a service and service management picks up from project management, preferably with due protocol and acceptance.  

[ITIL](http://www.itil-officialsite.com/) is a widely used standard for service management.  Large organisations that use ITIL typically would use PRINCE2 as the project management methodology to enable project delivery within known budgets and timelines.  Agile development methods are proving to be better at providing quality, meritocracy and skill rentention in software development.

At one client, we had the challenge of explaining how these will all work together.  Here is the sketch I used (with permission):
<!-- more -->

![]({{site.url}}/assets/2011/itil-p2-scrum.jpg)

* Agile development techniques are used to build and deliver components that correspond to a PRINCE2 work package. These are termed 'Dev' scrums.
* Agile 'sprints' or 'scrums' are also used to build configurations (environments, scripts, tests) etc. that are required for ITIL service transition and acceptance. These are termed 'IT' sprints.
* A PRINCE2 stage lifecycle should align with the service delivery cycle.

This approach helped us to find issues earlier and align delivery of developed components and infrastructure as a coherent service that could then be taken over by service management. 
