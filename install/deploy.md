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
the software.

# Deploying to the webapp

To deploy and start the web app, the general process is:

{:lang='bash'}
	scp CloudCoderWebServer/cloudcoderApp.jar username@server:/some/path
	ssh username@server
	cd /some/path
	java -jar cloudcoderApp.jar start

Replace `username` with the user account under which the webapp will run,
which can be any user account.  Replace `server` with the full hostname
(e.g., `cs.unseen.edu`) of the webapp server.  Replace `/some/path` for
the path of the directory in which the webapp will run.

If all goes well, you should now be able to open a web browser with the
URL

	https://server/cloudcoder

and see the CloudCoder login page.

If errors occur, check `/var/log/apache2/error.log` and `/some/path/logs/cloudcoder.log`.

## Stopping the webapp

To stop the webapp, run

{:lang='bash'}
	ssh username@server
	cd /some/path
	java -jar cloudcoderApp.jar shutdown

# Deploying to the build server

To deploy the builder server software:

{:lang='bash'}
	scp CloudCoderBuilder/cloudcoderBuilder.jar username@server:/another/path
	ssh username@server
	cd /another/path
	java -jar cloudcoderBuilder.jar start

Replace `username`, `server`, and `/another/path` as appropriate.
As with the webapp, `username` is the user account under which the build
server software will run, which should be an unprivileged account.
`server` is the hostname of the build server.  `/another/path` is the
directory in which the build server software will run.

You can check `logs/builder.log` for startup messages.  If you see messages that
read `Connected!` then the build server has successfully connected to the webapp
and is ready to download and test submissions.

## Stopping the build server

To stop the build server, run

{:lang='bash'}
	ssh username@server
	cd /another/path
	java -jar cloudcoderBuilder.jar shutdown
