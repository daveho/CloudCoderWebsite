---
layout: default
title: Provision and Configure Servers
---
To deploy CloudCoder, you will need two Linux servers: the
*webapp server* and the *build server*.

*Note*: you can probably use another Unix variant such as
FreeBSD or Solaris rather than Linux, but CloudCoder is not
tested on non-Linux platforms, so you might encounter issues.

The webapp server
=================

The webapp server runs the CloudCoder web application, and
hosts the database where CloudCoder will save information about
courses, problems, users, and student submissions.

Minimum requirements:

* 512M or more of RAM
* single-core CPU
* 8G of disk space
* port 443 open (for SSL)
* an SSL certificate

The minimum requirements should be adequate for up to 150
concurrent users.

The webapp server can be a virtual machine.  If your IT department
can set up a Linux virtual machine for you, this is a good option.
[lowendbox](http://www.lowendbox.com/) is a good resource for finding
an inexpensive hosting service.  Cloud hosting services such
as [Amazon EC2](http://aws.amazon.com/ec2/) are also a good choice.
