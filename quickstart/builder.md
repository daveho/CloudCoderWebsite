---
layout: default
title: Deploy the CloudCoder builder ("the builder")
---
[Prev](deploy.html) | [Next](commands.html)

# The CloudCoder builder or build server

The CloudCoder builder or build-server is the process that tests
student submissions against test cases.  Some notes:

### You need gcc/g++ to assign C/C++ exercises

To build C/C++ programs, the builder requires gcc/g++ to be on the
path of the account running the builder.

### Each builder must run in its own directory
DO NOT START THE BUILDER IN THE SAME FOLDER AS THE WEBAPP.

You can run multiple builders to scale up to larger loads.
However, you should create a separate folder for each builder.  You
can use the same cloudcoderBuilder.jar (by symlinks or by specificying
a relative or absolute path to find the file).

### It is not recommended, but you _can_ run the builder on the same
    machine as the server.

We don't recommend running the builder on the same machine as the
server.  But, it will work well to try out the system, for small
classes where load is not as much of an issue, or for virtual machines
that have access to a lot of cores.

### Starting and stopping the builder

First, make sure that you are not in the same directory where you
started the server.  If this is the first time starting the builder,
you should be in a new folder.

To start the builder:

	java -jar cloudcoderBuilder.jar start

And to shutdown the builder:

	java -jar cloudcoderBuilder.jar shutdown


