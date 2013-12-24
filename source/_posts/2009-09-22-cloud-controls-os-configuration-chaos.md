---
layout: post
title: Cloud Controls OS Configuration Chaos
tagline: one area where Cloud really helps
date: 2009-09-22 23:10:00+00:00
tags: [cloud, administration, configuration]
category: management
comments: false
---
Just as hardware became irrelevant a few years ago, we are about to make the operating system irrelevant with cloud computing.  

Servers were commoditized and put in farms, and their resources used and re-used with virtual machines.  Ubiquitous open source software and maturing web services were the final pieces of the puzzle, and clouds now allow us to design and deploy an application whose components may run on different machines, all connected by a single thread: the IP address!

The application is king!  The server hardware, virtualization technology and operating system have just become wrappers around the application.  The application consumes their resources and provides services.

So, where does configuration fit in?  Configuration was required to upgrade and optimise applications, improve their security or performance, or to make multiple instances or components live side by side without stepping on each others' toes. And yes, working with data structure migration, data retrieval and backup, which are not yet as commoditized but we are well on the way there.

<!-- more -->

How have the industry giants played this:  IBM has hooked up with Amazon EC2 while it works out its Cloudburst approach, Oracle bought Sun, and Microsoft saw an opportunity to enclose its proprietary operating system within a VM.  People saw pigs fly as Microsoft contributed GPL code to the Linux kernel, providing hooks for its virtualization technology.  So you see where I am going with this - it will not matter which OS is running the application, as long as the produced services are usable.  Operating systems will live or die based on the amount of stability they can provide to the application stack.  So:  IBM saw the opportunity to take the game to a higher level.  Oracle found a thought leader whose HW/OS will form a wrapper around Oracle's app-enabling technology, and they have just announced the Sun Cloud.  Microsoft sees it as an opportunity for people to not see the proprietary nature of the OS that runs apps built on proprietary MS technologies such as .NET, making them portable for all intents and purposes.

Expect to see a upcoming improvement in VM packaging technology, JVM embedded more into specific operating systems, and data semantic tools.  Upgrading an app would then just be building a new optimized VM image around the new app, and throwing the image it into the cloud, asking it to connect to existing data and upgrade the data structures as it sees fit.

Your friendly system administrator may not even know which operating system ends up executing the machine instructions on the CPU.  No twiddling, no configuration, nothing.

