---
layout: post
title: Resilient Crowd, Jira and Confluence on Amazon EC2 and RDS
tagline: experimenting with Amazon AWS EC2
date: 2011-12-11 23:10:00+00:00
tags: [crowd, cloud, aws, jira, confluence, amazon, ec2]
category: architecture
comments: false
---
**This page is out-of-date.**  Atlassian has come out with cloud pay-as-you-go pricing [(OnDemand)](http://www.atlassian.com/software/ondemand/overview) which is now recommended instead of the 10-user license mentioned below.
<!-- more -->
These are three tools that I cannot do without, and thanks to new Atlassian licensing options, I don't have to do without them.  Based on emerging cloud philosophy, I don't want to worry about routine things, and will let the cloud take care of as much as possible. Keeping this principle in mind, let us look at our topology:

1. Assume DNS and LDAP exist somewhere -- out of scope of this discussion.  DNS and LDAP are the keys to the kingdom, and healthy paranoia dictates that they are hosted separately.
2. Our data would be stored in a small [Amazon RDS](http://aws.amazon.com/rds/) instance, which is basically a MySQL machine with controlled parameters and access.  We do not want to worry about backups, standbys etc.  Let the cloud take care of it.
3. For the four applications that we are going to deploy, we will use an existing Linux distribution that can be booted off a virtual disk and can be saved back to it!  Amazon calls this an [EBS (Elastic Block Storage)](http://aws.amazon.com/ebs/) [AMI (Amazon Machine Image)](http://en.wikipedia.org/wiki/Amazon_Machine_Image).  Ubuntu is very serious about the cloud and we will use its 10.04 (Lucid Lynx) EBS image as a starting point.  Since we are going with a small machine, and they are only available in 32-bit yet, we will go for the [Ubuntu 10.04 32-bit server](http://developer.amazonwebservices.com/connect/entry.jspa?externalID=3102).

I will try to keep things at an intermediate complexity level, so that even if you are not familiar with the Amazon Cloud, you can follow along, and clarify concepts by clicking on the links.  Also, based on security principles (and the secure [multi-factor authentication](http://aws.amazon.com/mfa/) by Amazon), any techniques that you may have learned in which you put your access keys on one cloud machine in order to access another, should be forgotten.

1. **Principle 1:** Let the cloud handle as many routine things as it can, and follow its lead instead of fighting with it.
2. **Principle 2:** Your access key, secret key and certificate private key should be with you, and never on any cloud machine.
3. **Principle 3:** Unless you need redundancy and serving speed on a global scale, or you want to hedge against your Cloud provider melting down, keep all your cloud instances in one availability zone.

If you do not have one, create an EC2 account, and get yourself -- 
* Two elastic IPs, 
* One Security Group called 'apps' in addition to the default one, and 
* an EBS volume for your app data (50 GB is a good start) called `/dev/sdf`.

The pages below contain the general technical flow and discussion and, in addition, I will try to mention how redundancy and reliability can be designed and built into the topology.  In this way, the system administrator's approach to availability and performance becomes different and less complex.

Next: [Setting up the RDS Database Instance]({{site.url}}/architecture/2011/12/12/setting-up-the-rds-database-instance/)
