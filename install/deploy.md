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

# Import the database

Before the webapp will be able to run, you will need to import
the initial database contents.  Run the commands:

	scp CloudCoder/resources/cloudcoder-schema.sql cloud@server:
	ssh cloud@server
	mysql --user=cloudcoder --pass cloudcoderdb < cloudcoder-schema.sql

The command above refers to some choices you made when
you [provisioned the servers](servers.html):

* `cloud` is the user account under which the webapp will run
* `server` is the full hostname (e.g., `cloudcoder.unseen.edu`) of the webapp server
* `cloudcoder` is the database username
* `cloucoderdb` is the database name

Note that the database only needs to be imported once.

# Deploying to the webapp

To deploy and start the web app, the general process is:

	ssh cloud@server 'mkdir -p webapp'
	scp CloudCoderWebServer/cloudcoderApp.jar cloud@server:webapp
	ssh cloud@server
	cd webapp
	java -jar cloudcoderApp.jar start

Again, `cloud` is the user account and `server` is the full hostname
of the webapp server.

If all goes well, you should now be able to open a web browser with the
URL

	https://server/cloudcoder

and see the CloudCoder login page.

If errors occur, check `/var/log/apache2/error.log` and `webapp/logs/cloudcoder.log`.

## Stopping the webapp

To stop the webapp, run

	ssh username@server
	cd webapp
	java -jar cloudcoderApp.jar shutdown

# Deploying to the build server

To deploy the builder server software:

	scp CloudCoderBuilder/cloudcoderBuilder.jar username@server:/another/path
	ssh username@server
	cd /another/path
	java -jar cloudcoderBuilder.jar start

Replace `username`, `server`, and `/another/path` as appropriate.
(In this case, `server` should be the server you're using as the build
server, not the webapp server.)
As with the webapp, `username` is the user account under which the build
server software will run, which should be an unprivileged account.
`server` is the hostname of the build server.  `/another/path` is the
directory in which the build server software will run.

You can check `logs/builder.log` for startup messages.  If you see messages that
read `Connected!` then the build server has successfully connected to the webapp
and is ready to download and test submissions.

## Stopping the build server

To stop the build server, run

	ssh username@server
	cd /another/path
	java -jar cloudcoderBuilder.jar shutdown
