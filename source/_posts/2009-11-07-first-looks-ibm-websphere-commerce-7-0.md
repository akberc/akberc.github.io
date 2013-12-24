---
author: akberc
comments: false
date: 2009-11-07 16:39:00+00:00
layout: post
slug: first-looks-ibm-websphere-commerce-7-0
title: 'First Looks: IBM WebSphere Commerce 7.0'
wordpress_id: 194
categories:
- eCommerce
- server
- websphere
tags:
- commerce
- websphere
---
I took IBM WebSphere Commerce 7.0 for a spin over the past couple of days.  First impressions:
<!-- more -->

  * generally, it had to keep up with the overall WebSphere versioning scheme, but in reality it is more like 6.5 than 7.0 (or maybe even 5.8 if one believes that 6.0 should have been 5.7).  It pulls together all the 6.0 feature packs and provides new incremental features, primarily social commerce and targeted marketing tools.
  * technology updates, including a long-overdue database abstraction layer and running on WAS 7.0 - but still short of what is state-of-the-art in the JEE world.  The ORM layer is still too dependent on underlying primary keys system.
  * dev environment works better, even with a publishing failure during installation, and it is more self-contained with XML and properties within the EAR
  * although we have not done any integrations yet, my opinion is that integration with other systems and back-ends should become easier and more standards-compliant

To be fair to IBM, they have done a good job, and not tinkered much with the market leader, but maybe they should start working on the next major release with a grounds-up re-design:
	
  * with Hibernate-style ORM and inversion-of-control architecture with configuration and interface specification through annotations and much less configuration.  This will also simplify data load and reporting.
  * a built-in portlet container (without the overhead of a full-blown Portal Server) and portlet-based tools replacing the who-knows-what-based admin, org and acc consoles, the OpenLaszlo-based Management centre and the Eclipse-based Sales Centre.  UI consolidation is way over-due.
  * a JSR299 (web beans) based framework with annotation-based security hooks that should get rid of all that ugly Struts-database command integration.

Well, we can dream, can't we?

