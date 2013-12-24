---
layout: post
title: Eclipse and OSGi - p2 is Broken in Ganymede
tagline: ... long since fixed
date: 2009-04-22 23:10:00+00:00
tags: [eclipse, osgi, p2, modularity, dependency]
category: development
comments: false
---
**UPDATE:** Most of these issues are fixed in Ganymede SR2, and I am using the OSGi update mechanism now.

<!-- more -->

[Eclipse](http://www.eclipse.org/) is a great tool with its main strength being its modular architecture.  Everything is a module, and modules can bee updated from within Eclipse.  This architecture propelled Eclipse into the leading IDE for Java and J2EE developers, as well as for other languages and platforms.  Vendors who have taken advantage of this architecture to base their IDEs on Eclipse are the who's who of the software world.

Soon enough, with versions and sub-projects, updates became a hassle. So, we ended up with the 'train release' concept from Eclipse - Europa and then Ganymede - a release of various plug-ins and modules that have been tested together. With the excellent experience of Europa behind me, I replaced it with Ganymede - so high were the expectations that I did not keep a backup.

Along comes the popularity of [OSGI](http://www.osgi.org/) as a universal software component architecture.  Eclipse could only have become better with it, but unfortunately, it was released while it was still not user-friendly and did not enhance productivity.  I was spending a lot of time reconciling updates, and many times, P2 (as the Eclipse OSGi toolset is called) just wouldn't leave me with a way out.  With a DSL Internet connection, it would take hours or just hang while resolving dependencies, downloading dependency files from every plugin site.  In short, it was a nightmare, and to top it off, it did not run in the background.

Looking around, it was apparent that the old plugin manager - 'Classic Update' - was still available in all Ganymede versions but that it could only be activated through the Preferences menu in the SDK version.

And then I found the way to remove p2.  It is official - right from Eclipse web sites - and it works: [http://wiki.eclipse.org/Equinox_p2_Removal](http://wiki.eclipse.org/Equinox_p2_Removal) 

There is also an [automated script](https://bugs.eclipse.org/bugs/attachment.cgi?id=110125) available, but I was not brave enough to run it, although I used the `config.ini` and `eclipse.ini` files included in it.  Also, I moved the directories and files to another folder instead of deleting them.  This way I had an easy way out in case this did not work.  But it worked very well, and I had a reliable speedy Eclipse back.  However, I have an invalid configuration which means the vaunted p2 did not do its job properly while it was in charge.

We'll have to wait for a more stable version of OSGi in Eclipse.


