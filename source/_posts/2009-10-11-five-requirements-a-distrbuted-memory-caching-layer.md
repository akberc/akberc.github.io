---
author: akberc
comments: false
date: 2009-10-11 19:20:00+00:00
layout: post
slug: five-requirements-a-distrbuted-memory-caching-layer
title: Five Requirements of a Distrbuted Memory Caching Layer
wordpress_id: 193
categories:
- cloud
- server
tags:
- cache
- distributed
- memory
- selection
---
Caching provides persistent business data  and volatile session data from memory instead of from database and/or disk access.  This improves performance.  Clusters of application servers also provide performance and scalability.  The two techniques clash as one application server's cache is not in sync with others' caches.

A solution for this clash is through Network-Attached Memory (NAM), which is very similar in role to a SAN (Storage Area Network) that is used for shared disk access.  External memory (spread over one or more cache servers) is made available to each application server, who think of it as their own memory.  Resources are not wasted and each application server's view of cached content is identical – as it is in fact the same data in memory that is visible to all.

<!-- more -->

**Read-only, Write-through and Write-behind**

Just as a SAN provides continuous service even when individual disks or arrays crash, NAM should provide this shared memory even when one of the NAM servers crashes or is taken out of service.  This is distributed caching, or a data grid.  Generally, these are read-only, with write-through (writes pass through directly to disk or DB, updating the cache), and rarely, they may be write-behind: accept data commits from applications and 'write-behind' so that the application finishes its commit or update, oblivious to whether the data may not have been written to disk or database yet, and the grid will write it out when it deems appropriate.

**Short-listing Products**

Common products out there are Terracotta, Gigaspaces, JBoss Infinispan and Oracle Coherence

Working on a real-life high-performance portal, I came up with these requirements to create a short-list:

  1. Capability to cache database record objects, service invocation return objects, sessions and session objects.  Objects include object graphs.
  2. Transparent to applications, portal and any framework.  The portal platform should be able to function completely WITHOUT the distributed cache, and with little configuration changes if required.
  3. Should have no startup latency – cache warming should be accomplished using other techniques.
  4. Should be always available.  Failover of nodes providing the distributed cache, and their load-balancing, should be automatic.
  5. Should require NO code or configuration changes when new portal applications or web services are added.

