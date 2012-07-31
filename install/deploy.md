---
layout: default
title: Deploy CloudCoder
---
[Prev](build.html) [Next](course.html)

This page describes how to deploy the CloudCoder software to the
webapp server and build server.

Recall that the result of the [previous step](build.html) was two
jar files.  These jar files are completely self-contained: all you need
to do is copy them to the server.  Once copied to the server,
simple commands (described below) allow you to start, control, and stop
the webapp and builder processes.

# Copying the webapp to the server

The webapp is a single executable jar file.  Copy it to the webapp
server with the following commands:

	ssh cloud@server 'mkdir -p webapp'
	scp CloudCoderWebServer/cloudcoderApp.jar cloud@server:webapp

# Import the database

Before the webapp will be able to run, you will need to import
the initial database contents.  Run the following commands:

	ssh cloud@server
	cd webapp
	java -jar cloudcoderApp.jar createdb

You will be prompted to choose a name and password for your CloudCoder
user account, and to enter an institution name.

Note that the database only needs to be imported once

# Starting the webapp

To start the web app:

	ssh cloud@server
	cd webapp
	java -jar cloudcoderApp.jar start

Again, `cloud` is the user account and `server` is the full hostname
of the webapp server.

If all goes well, you should now be able to open a web browser with the
URL

	https://server/cloudcoder

and see the CloudCoder login page.  You should be able to log in
using the username and password you chose when you imported the
database.

If errors occur, check `/var/log/apache2/error.log` and `webapp/logs/cloudcoder.log`.

## Stopping the webapp

To stop the webapp, run

	ssh username@server
	cd webapp
	java -jar cloudcoderApp.jar shutdown

# Deploying the build server

To deploy the builder server software:

	ssh username@server 'mkdir -p builder'
	scp CloudCoderBuilder/cloudcoderBuilder.jar username@server:builder
	ssh username@server
	cd builder
	java -jar cloudcoderBuilder.jar start

Replace `username` and `server` as appropriate.
(In this case, `server` should be the server you're using as the build
server, not the webapp server.)
As with the webapp, `username` is the user account under which the build
server software will run, which should be an unprivileged account.
`server` is the hostname of the build server.

You can check `logs/builder.log` for startup messages.  If you see messages that
read `Connected!` then the build server has successfully connected to the webapp
and is ready to download and test submissions.

## Stopping the build server

To stop the build server, run

	ssh username@server
	cd builder
	java -jar cloudcoderBuilder.jar shutdown
