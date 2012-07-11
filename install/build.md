---
layout: default
title: Building the CloudCoder Software
---
[Prev](servers.html) [Next](deploy.html)

This page describes how to configure and build the CloudCoder software.

You can build the CloudCoder software on any computer (for example,
the computer you normally use for development.)  You could also
use whatever computer you are using as your build server
(since it will be running Linux and  is probably relatively powerful.)

# Prerequisites

To build CloudCoder, you will need the following software:

* git
* JDK 1.6 or later
* Ant
* perl
* GWT SDK 2.4 or later

On Debian or Ubuntu Linux, you can install everything except the GWT
SDK using the command

	sudo apt-get install git openjdk-6-jdk ant

The GWT SDK can be downloaded from

> <https://developers.google.com/web-toolkit/versions>

Make sure you get version 2.4 or later.  Note that if you have the
[Google Plugin For Eclipse](https://developers.google.com/eclipse/docs/download) installed,
the SDK is included, meaning that you don't need to download it separately.
Look in the `plugins` directory in your eclipse installation
for a directory whose name begins with `com.google.gwt.sdk`.

# Check out the code

Use git to check out the CloudCoder source code:

	git clone git://github.com/daveho/CloudCoder.git

Alternately, you can fork the repository on github (at <https://github.com/daveho/CloudCoder>)
and then clone your fork.  This is the best option if you plan to make any changes
to the code.

Change directory into the directory you just checked out:

	cd CloudCoder

# Configure CloudCoder

Before you build CloudCoder, you need to enter all of the configuration
information CloudCoder will need to run.  Run the command:

	./configure.pl

You will be prompted with a series of questions.  Here is an example session:

	Welcome to the CloudCoder configuration script!
	Please enter the information needed to configure CloudCoder for your system.
	You can just hit enter to accept the default value (if there is one).
	
	Where is your GWT SDK installed (the directory with webAppCreator in it)?
	==> /home/dhovemey/software/gwt-2.4.0               
	
	What MySQL username will the webapp use to connect to the database?
	==> cloudcoder
	
	What MySQL password will the webapp use to connect to the database?
	==> somepassword
	
	What MySQL database will contain the CloudCoder tables?
	[default: cloudcoderdb] ==> 
	
	What host will CloudCoder connect to to access the MySQL database?
	[default: localhost] ==> 
	
	If MySQL is running on a non-standard port, enter :XXXX (e.g, :8889 for MAMP).
	Just hit enter if MySQL is running on the standard port.
	==> 
	
	Which login service do you want to use (imap or database)?
	[default: database] ==>         
	
	What host will the CloudCoder webapp be running on?
	(This information is needed by the Builder so it knows how to connect
	to the webapp.)
	[default: localhost] ==> cs.unseen.edu
	
	How many threads should the Builder use? (suggestion: 1 per core)
	[default: 2] ==> 8
	
	What port will the CloudCoder webapp use to listen for connections from
	Builders?
	[default: 47374] ==> 
	
	What port will the CloudCoder web server listen on?
	[default: 8081] ==> 
	
	What context path should the webapp use?
	[default: /cloudcoder] ==> 
	
	Should the CloudCoder web server accept connections only from localhost?
	(Set this to 'true' if using a reverse proxy, which is recommended)
	[default: true] ==> 
	
	Write configuration file (local.properties)?
	[default: yes] ==> 
	Writing properties...Done!

Note that in the transcript above, many of the default options were chosen
(such as choosing `cloudcoderdb` as the database name.)  Just press enter
to accept a default option.

Make sure that you use the same MySQL username, password, and database name
that you specified when you [provisioned the servers](servers.html).

# Build CloudCoder

To build CloudCoder, just run the command

	./build.pl

The command will take a while to run, but when it finishes you will have
two jar files representing the deployable form of the software that
will run on the webapp server and the build server:

	CloudCoderWebServer/cloudcoderApp.jar
	CloudCoderBuilder/cloudcoderBuilder.jar
