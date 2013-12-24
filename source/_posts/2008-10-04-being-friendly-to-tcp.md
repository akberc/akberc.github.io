---
layout: post
title: Being Friendly to TCP
tagline: things learnt while managing a large infrastructure program
date: 2008-10-04 15:10:00+00:00
tags: [network, streaming, tcp/ip, tcp, udp]
category: architecture
comments: false
---
UDP traffic should not affect TCP connections when there is a contention for bandwidth.

<!-- more -->

###What is TCP-Friendliness?
UDP and other continuous streaming transports are becoming more common on the Internet as multimedia, telephony and P2P applications start to use larger and larger portions of available bandwidth.

One of the better definitions of TCP-friendliness is as follows: "a flow is TCP-friendly if other TCP connections sharing the same bottleneck link as it do not receive less bandwidth in the long term than they would receive if the flow in concern is also a TCP connection possibly with a short Round Trip Time(RTT)." [1](#footnotes)

TCP is well-behaved in terms of transfer reliability and has built-in congestion control [2](#footnotes). Non-TCP flows are commonly used when such niceties are not required and a simpler data push/pull serves the job. However, as such flows take up more and more of the bandwidth, TCP connections start to lose out. The goal of TCP-friendliness is to allow non-TCP data flows to consume as much bandwidth as a TCP connection would and not much more, thus implementing a "fair" regime of resource-sharing. Since non-TCP transport protocols are usually less sophisticated and more varied, it would not be practical to prescribe congestion control WITHIN those protocols. It is much more feasible to prescribe such actions at the IP routing level.

Active Queue Management is just one of the techniques used to accomplish this within TCP-friendly routers. Such routers actively monitor traffic and exchange information and throttle certain types of traffic to achieve TCP-friendliness. [3](#footnotes)

This is an active area of research and proposed solutions still lag behind requirements. Sally Ford [2](#footnotes) is a prominent researcher in this area and some of her research papers can be found [here](http://www.icir.org/tfrc/).

<a name="footnotes">&nbsp;</a>
###References
<p>[1] http://cairo.cs.uiuc.edu/~binyu/writing/binyu-497-report.pdf</p>
<p>[2] Kurose and Ross, Computer Networking, Third Edition, p.298</p>
<p>[3] http://www.cs.wpi.edu/~claypool/papers/queue-law/</p>

