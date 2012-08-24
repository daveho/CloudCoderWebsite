---
layout: default
title: Deploy the CloudCoder webapp (the server)
---
[Prev](configure.html) | [Next](builder.html)

This describes how to deploy CloudCoder for the first time.  Once CloudCoder is installed, you can run many of these comamnds by themselves to manage the system.

# Deploy CloudCoder

### Prepare a directory for the webapp

Create a fresh folder and put cloudcoderApp.jar inside it.  This should probably not be the same folder where you configured cloudcoder.  A good name for this folder is cloudcoder.

All commands in this section should be run in this directory.

### Register students

In the cloudcoder folder, register students by running this command:

	java -jar cloudcoderApp.jar registerstudents

This command will prompt for the name of a tab-delimited text file.  This file should have a number of tab-delimited lines in the following format:

username	firstname	lastname	email	password	section

The section is optional (it will default to 101 if you leave it out)

_There is currently no way to change passwords, so you will have to email passwords to the students_

### Starting the server

To start the server:

	java -jar cloudcoderApp.jar start

This will create some files and a log directory.

### Shutting down the server

To shutdown the, server, run this command:

	java -jar cloudcoderApp.jar shutdown

If CloudCoder doesn't exit after two or three minutes, you can kill the process.



