---
layout: post
title: Setting up the RDS Database Instance
tagline: experimenting with Amazon AWS EC2
date: 2011-12-12 23:10:00+00:00
tags: [crowd, cloud, aws, jira, confluence, amazon, rds]
category: architecture
comments: false
---
**Update:** Amazon AWS RDS can now be configured from the AWS Web console
<!-- more -->
Although the RDS is a service and we are not supposed to think of it as a machine, it is just like an EC2 instance.  We have to use the command-line tools, as RDS instances --do not show up under-- the [EC2 console](https://console.aws.amazon.com/ec2/home) *(they do as of 2010-05-26)* or in other tools like [ElasticFox](http://developer.amazonwebservices.com/connect/entry.jspa?externalID=609).  This toolkit should run on your local machine, and without going into too much detail, please make sure that the following environment variables are set -- here is an excerpt of a shell script that I use to set up my RDS environment and I run it in the folder where I unzipped the [RDS command-line tools](http://developer.amazonwebservices.com/connect/entry.jspa?externalID=2928)
{% highlight html %}
export AWS_RDS_HOME=`pwd`
export JAVA_HOME=/usr/lib/jvm/java-6-openjdk/jre
export AWS_CREDENTIAL_FILE=~/.ec2-credential-file
export PATH=$PATH:$AWS_RDS_HOME/bin
export EC2_REGION=eu-west-1b
{% endhighlight %}

Note that there a few ways to access Amazon Web Services, one of which uses the access key and credentials, and  I leave my credentials file hidden in my home folder.  It should look like this:
{% highlight html %}
AWSAccessKeyId=AAAAAAAAAAAAAAAAAAAAAAAAAA
AWSSecretKey=ZZZZZZZZZZZZZZZZZZZZZZZZZzZZ
{% endhighlight %}

Note that redundancy is provided through automated backups, retention periods, snapshots, and multi-AZ (availability zones) provided by the Amazon AWS Cloud itself.

We will create the RDS instance, change some server parameters and allow access to it from the cloud instance(s) that will run the application:<br/>
{% highlight html %}
rds-create-db-instance ZZZZZ --allocated-storage NN --db-instance-class db.m1.small --engine MySQL5.1 --master-username MMMM --master-user-password xxxxxxxxxx --backup-retention-period 7 --availability-zone eu-west-1b --headers

# WAIT UNTIL INSTANCE IS CREATED (use rds-describe-db-instances to view progress)

# Set up server for UTF-8 operations
rds-create-db-parameter-group utf8 --engine mysql5.1 --description "Parameters for UTF-8"
rds-modify-db-parameter-group utf8 --parameters="name=character_set_server, value=utf8,method=immediate"
rds-modify-db-instance appsdb --db-parameter-group-name utf8

# Reboot the instance
rds-reboot-db-instance appsdb

#WAIT UNTIL parameters are applied and reboot is complete

# Allow access from the EC2 application instances.  We assume that we arleady have an EC2 security group called apps.  It can be anything, and contain anything, as long as it is the security group that is (or will be) applied to the apps cloud instances:

rds-authorize-db-security-group-ingress Default --ec2-security-group-name apps --ec2-security-group-owner-id 999988881111

# Ensure that all went well.  Some columns have been ommitted.  Make a note of the DNS names.  The mySQL client and the applications will refer to it
rds-describe-db-instances --headers
DBINSTANCE  DBInstanceId   ~~~~  Status     Endpoint Address                          Port  AZ          Backup Retention  Multi-AZ
DBINSTANCE  social               available  appsdb.xxxxx.eu-west-1.rds.amazonaws.com  3306  eu-west-1b  7                 n       
      SECGROUP  Name     Status
      SECGROUP  default  active
      PARAMGRP  Group Name  Apply Status
      PARAMGRP  utf8        in-sync
{% endhighlight %}

