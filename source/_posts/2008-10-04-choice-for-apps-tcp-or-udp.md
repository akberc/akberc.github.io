---
layout: post
title: Choice for Apps - TCP or UDP
tagline: for high-performance native apps
date: 2008-10-04 14:10:00+00:00
tags: [network, tcp, udp, apps, multimedia, video, audio]
category: architecture
comments: false
---
**Abstract:** Describes the main points of difference between UDP and TCP as a transport for application development. When should one be chosen over another and why? Provides some examples.

<!-- more -->

##UDP and TCP in application development
The popularity and ubiquity of the UDP/TCP/IP protocol stack has provided application developers with a comparatively simple and almost universal network interfacing API (application programming interface) in many high-level languages. The basic concepts that the programmer needs to understand are:
1. Difference between various "sockets" (Unicast UDP, Multicast UDP, TCP).
2. Difference between client sockets and server sockets.
3. Allocating and disposing of system resources (memory, port numbers, sockets etc.) even in the case of errors.
4. Basic network addressing and DNS knowledge.
5. Reading and writing to sockets and various language-specific constants.

##UDP vs TCP
Armed with this information, the programmer can now choose which type of transport protocol (UDP or TCP) to use.

###UDP
1. connection-less
2. no guarantee of packet arrival or order
3. no congestion control mechanisms
4. basic checksum integrity
5. potentially higher throughput.

###TCP
1. connection-full and stateful
2. guaranteed orderly arrival
3. congestion control
4. higher integrity checks
5. less throughput due to TCP connection overhead.

Generally, applications should use UDP when one or more of the following apply:
1. packet losses can be tolerated
2. Bandwidth usage is more important than reliability
3. payload is contained within a single packet or only basic multi-packet assembly is required.
4. information order is not important
5. multicasting is desired

Generally, applications should use TCP when one or more of the following apply:
1. end to end reliability of transport is required.
2. data integrity and order is more important than bandwidth consumption
3. payload can span many packets and order is important
4. pipelining can be leveraged

##Examples

###1. Network Backup Application:
This application has a client piece that is installed on workstations and allows the user to configure backup parameters and initiate the backup. A server piece runs on the central computer and responds to backup requests. It reads the parameters, updates existing backups, provides with last-changed information back tot he client and then stores new backup files.

This application needs to be programmed using TCP. Although we require maximum bandwidth utilization, we also need absolute reliability and acknowledgement of receipt from the server. 

###2. Car Counter
This is an embedded application that runs on an embedded Linux device with a camera and an 802.11g transmitter built-in. This device runs on batteries and is placed on a road-side and its counts cars that pass it by. It is used portable and is used to monitor car traffic congestion and trigger traffic signal alignment. Many such devices feed into a central computer and also send signals to neighbouring taffic signal regulators.

This application should use UDP. Minor losses can be tolerated and data can be received in any order, as it only serves to increment. The information sent is very small and UDP multicasting can also be utilized.

