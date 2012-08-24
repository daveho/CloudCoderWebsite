---
layout: default
title: CloudCoder commands to manage your installation
---
[Prev](builder.html) | [Next](update.html)

# Complete list of command-line options for managing your CloudCoder installation

### Configure new cloudcoder properties

There are two situations where this would be useful:

1.  You want to change the settings of an existing CloudCoder
installation
2.  You want to apply existing configuration properties to a new
binary distribution (we may distribute bug fixes, new features, etc)

In either case, you should shutdown your cloudcoder installation
before re-configuring a binary jarfile.

This should only necessary if a new binary distribution is available
(bug fixes, new features, etc).  You should shutdown your cloudcoder
installation before re-configuring it.

First, edit the cloudcoder.properties file, then copy it into the folder containing `cloudcoderApp.jar`.  Then run this command:

	java -jar cloudcoderApp.jar configure

### List configuration properties

From the directory containing `cloudcoderApp.jar`, run this command:

	java -jar cloudcoderApp.jar listconfig

### Register students

In the folder containing `cloudcoderApp.jar`, register students by running this command:

	java -jar cloudcoderApp.jar registerstudents

This command will prompt for the name of a tab-delimited text file.  This file should have a number of tab-delimited lines in the following format:

`username	firstname	lastname	email	password	section`

The section is optional (it will default to 101 if you leave it out)

*There is currently no way to change passwords*

### Create a new user account (student or instructor)

	java -jar cloudcoderApp.jar createuser

Then follow the prompts.

### Start the server

In the folder containing `cloudcoderApp.jar`:

	java -jar cloudcoderApp.jar start

### Shutdown the server

In the folder containing `cloudcoderApp.jar`:

	java -jar cloudcoderApp.jar shutdown

### Create the cloudcoder database (Should only be done once!)

In the folder containing `cloudcoderApp.jar`:

	java -jar cloudcoderApp.jar createdb

### Start the builder

**
