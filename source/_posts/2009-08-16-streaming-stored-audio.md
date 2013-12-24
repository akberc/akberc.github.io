---
layout: post
title: Streaming Stored Audio
tagline: ...probably out of date
date: 2009-08-16 23:10:00+00:00
tags: [network, streaming, tcp/ip, tcp, udp, audio, video]
category: architecture
comments: false
---
When streaming stored audio, does it make sense to run the application over UDP or TCP at the transport layer? Here is a brief summary based on the the products of RealNetworks and Microsoft:

<!-- more -->

Let us say we have stored audio that we want to stream. The two most common problems are:
1. The audio may or may not be stored in a compressed state. Compressed audio is less loss-tolerant than uncompressed purely due the reason that lossy compression (most common types of audio 	compression are lossy) has already taken out a lot of the data that would have been undetectable by the human ear. 
2. The time-sensitivity of stored audio is less than that of realtime audio [1](#footnotes) as the client application can cache part of the stream that is yet to play and hence have some tolerance.

###Streaming stored audio over UDP transport:
* ADVANTAGE: It does not have the overhead of TCP connection management overhead, and can result in better quality 
* ADVANTAGE: It can use multiple ports and much faster speeds. 
* DISADVANTAGE: It still needs some type of control protocol -- over another UDP port or a TCP connection. 
* DISADVANTAGE: It cannot travel well over firewalls, NAT (network address translation) and some type of routers. 
* DISADVANTAGE: If the stored audio is lossy compressed, potential packet loss may reduce quality to below an arbitrary threshold. 

###Streaming stored audio over TCP transport
* ADVANTAGE: For lossy stored audio, it can guarantee a minimum level of sound quality. 
* ADVANTAGE: It can pass over firewalls and NAT setups much more easily. 
* ADVANTAGE: It does not require an extra control channel. TCP itself provides the control and application-level protocols can piggyback on to the same channel. 
* DISADVANTAGE: Due to TCP connection management overhead, its throughput may be lower. 
* DISADVANTAGE: It is highly impractical to use multiple TCP connections for the same stream. 

###REALNETWORKS 
At the application level (client) RealNetworks products support RTSP (Real Time Streaming Protocol) [2](#footnotes) for the control protocol and either RDT (a proprietary RealNetworks protocol) or RTP (Realtime Transport Protocol) as the data protocol [4](#footnotes). For backward compatibility, PNA (an older RealNetworks proprietary protocol) is still supported, both for control and data and we will not discuss this further.

RTSP runs as a HTTP-like protocol over one or more sequential TCP connections for the duration of the stream (state maintained on server). This is the first connection to be established and it helps in selecting a transport (UDP, multicast UDP or TCP) for the data protocol. In case of no other feasible option, the RTSP connection can also handle the data, although of a much lower quality. The preferred protocol for the data in the RealNetworks client (RealPlayer) is RDT over UDP, although it cleverly uses RTSP to find the ideal transport mechanism. Transport preference for the data part can be explicitly overriden in RealPlayer.

UDP is preferred as the transport by RealPlayer due to the better media quality (less overhead) and multiple port options available under UDP. RTP and RTCP, when running over UDP, take advantage of the
checksum capabilities of UDP. 

###MICROSOFT 
The Microsoft realtime protocol stack is very similar to that of RealNetworks [5](#footnotes). While older versions use the MMS (Microsoft proprietary protocol), newer versions use RTSP over either UDP or TCP. Again, UDP is preferred, but the transport can be overriden by user choice in the Windows Media Player.

Unique to Microsoft, the RTSP protocol piggybacking is used to deliver content, and like RealNetworks, HTTP can be used entirely, but obviously without some of the additional negotiating and control services provided by RTSP. 

<a name="footnotes">&nbsp;</a>
###References
<p>[1] Kurose and Ross, Computer Networking, Third Edition, p. 84,
figure 2.4 
</p>
<p>[2] http://www.rtsp.org/ 
</p>
<p>[3] http://www.ietf.org/rfc/rfc1889.txt 
</p>
<p>[4]
http://service.real.com/help/library/guides/productiong261/htmfiles/whatsnew.htm
</p>
<p>[5]
http://www.microsoft.com/windows/windowsmedia/serve/firewall.aspx 
</p>

