---
layout: default
title: Provision and Configure Servers
---
Prev | [Next](build.html)

To deploy CloudCoder, you will need two Linux servers: the
*webapp server* and the *build server*.
This page describes how to provision and set up these
servers.

*Note*: you can probably use another Unix variant such as
FreeBSD or Solaris rather than Linux, but CloudCoder is not
tested on non-Linux platforms, so you might encounter issues.

The webapp server
=================

The webapp server runs the CloudCoder web application, and
hosts the database where CloudCoder will save information about
courses, problems, users, and student submissions.
It will need to be available on the network(s) your students
will use to access CloudCoder.  Making it accessible from
the public internet is ideal (since that would allow students to
work anywhere), but you could also choose to make it available
only on your campus network.

Suggested server configuration:

* 512M or more RAM
* 2G or more disk space
* any modern CPU (single core is fine)
* port 443 open (for SSL)
* a DNS name (e.g., **cloudcoder.unseen.edu**)
* an SSL certificate (which must match the DNS name)

The suggested configuration should be adequate for around 150
concurrent users.

The webapp server can be a virtual machine.  If your IT department
can set up a Linux virtual machine for you, this is a good option.
[lowendbox](http://www.lowendbox.com/) is a good resource for finding
an inexpensive hosting service.  Cloud hosting services such
as [Amazon EC2](http://aws.amazon.com/ec2/) are also a good choice.
(An EC2 micro instance works well as a webapp server.)

If you use a hosting service, we recommend that you use Debian or
Ubuntu Linux.  For example, if you use Amazon EC2
Ubuntu Server 12.04 LTS is a good choice.

Webapp server configuration
---------------------------

Once your webapp server is available, you should install the following
software on it:

* JDK 1.6
* MySQL
* Apache2

On Debian or Ubuntu Linux, use the command:

	sudo apt-get install openjdk-6-jdk mysql-client mysql-server apache2

Make a note of the password you choose for the MySQL `root` user.

### Create a cloudcoder user account

You will want to create a dedicated user account for running the CloudCoder
web application.  Run the command:

	sudo adduser cloud

This will create a user called `cloud`.  When you [deploy the web application](deploy.html),
you will use this user account.

### Configuring MySQL

You will need to create a MySQL user account for the CloudCoder webapp
to use to communicate with the database.  Using the username
`cloudcoder` is a good choice.  To create the user, run the
command

	mysql --user=root --pass \
	--execute="create user cloudcoder identified by 'somepassword'"

Enter the password for the MySQL `root` user when prompted.
Replace `cloudcoder` and `somepassword` with the username and password you
want to use.

Next, create the database cloudcoder will use.  `cloudcoderdb` is a good choice,
but you can use any database name.  Run the command

	mysql --user=root --pass --execute="create database cloudcoderdb"

Finally, grant the cloudcoder user account permission to create tables:

	mysql --user=root --pass \
	--execute="grant all on cloudcoderdb.* to 'cloudcoder'@'localhost'"

Again, replace `cloudcoder` and `cloudcoderdb` with the username and
database name you chose previously.

### Configuring Apache2

The Apache2 web server will act as a front-end for the CloudCoder web
application.  In particular, it will accept requests via https
and dispatch them to the CloudCoder web application.

If you are using Debian or Ubuntu Linux, you will need to edit the
file `/etc/apache2/sites-available/default-ssl`.  This file should
begin with the line `<VirtualHost *:443>`.

Make sure the `ServerName` directive is specified correctly.
For example, if your hostname is `cloudcoder.unseen.edu`,
then it should be specified as

	ServerName cloudcoder.unseen.edu:443

Add a section to the top of the file (just below the `ServerAdmin` directive)
as follows:

	# Transparently proxy requests for /cloudcoder to the
	# CloudCoder Jetty server
	ProxyPass /cloudcoder http://localhost:8081/cloudcoder
	ProxyPassReverse /cloudcoder http://localhost:8081/cloudcoder
	<Proxy http://localhost:8081/cloudcoder>
	    Order Allow,Deny
	    Allow from all
	</Proxy>

Note that the port number mentioned in the example above (8081) is the
local port number the CloudCoder web application will listen on.

To make sure that `mod_proxy` is enabled, run the command

	sudo a2enmod proxy

At the bottom of the file, you will need to specify the locations of
your SSL certificates and private key.  For example,

	SSLEngine On
	SSLCertificateFile /etc/cert/cert.cer
	SSLCertificateChainFile /etc/cert/chain.cer
	SSLCertificateKeyFile /etc/keys/server.key

The example above assumes that certificates are stored in `/etc/cert` and the
server private key is stored in `/etc/keys`.  The server private key should
be a file readable only by `root`.  The "chain" certificate is the one
that establishes a chain of trust between a root CA and your server's certificate.

To enable Apache to server SSL requests, run the commands:

	cd /etc/apache2/sites-enabled && sudo ln -s ../sites-available/default-ssl

Apache should be restarted to make these configuration changes take effect:

	sudo service apache2 restart

The build server
================

The build server is the server that builds and tests student submissions.
It does *not* need to be accessible from a public network: it maintains
a network connection to the webapp server, and when the webapp has
a submission that needs testing, it is sent to the build server via this
connection.  So, you can provision the build server as
a physical PC that you place in a location that has a network connection
(your office, a server room, etc.)
You can also use a hosting service for the build server.

Depending on how many students will be using CloudCoder, you may want
to choose relatively powerful hardware for the build server.  A suggested
configuration is

* Quad-core or better CPU
* 8GB or more RAM

The build server requires the following software:

* JDK 1.6 or later
* gcc/g++ (if you will be assigning C/C++ problems)

To install this software on Debian or Ubuntu Linux:

	sudo apt-get install openjdk-6-jdk gcc g++
