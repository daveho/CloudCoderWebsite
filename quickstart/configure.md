---
layout: default
title: Configure the CloudCoder binaries
---
[Prev](mysql.html) | [Next](deploy.html)

# Configure CloudCoder

### Download the binaries

Download the pre-compiled webapp and builder binaries, along with the cloudcoder.properties configuration file:

* [cloudcoderApp.jar](http://cs.knox.edu/jspacco/cloudcoder/cloudcoderApp.jar)
* [cloudcoderBuilder.jar](http://cs.knox.edu/jspacco/cloudcoder/cloudcoderBuilder.jar)
* [cloudcoder.properties](http://cs.knox.edu/jspacco/cloudcoder/cloudcoder.properties)

### Configure the CloudCoder binaries

Put all 3 files your just downloaded into the same directory.

Enter the information for the [MySQL installation](mysql.html) you set up from the previous step into the cloudcoder.properties file.  The other settings can stay the same.

To configure your pre-compiled binaries with the configuration settings you just entered in your cloudcoder.properties, run this command:

	java -jar cloudcoderApp.jar configure

And follow the instructions.  This will copy the configuration properties from your cloudcoder.properties file into the two jarfiles.

### Create the cloudcoder database

Run this command:

	java -jar cloudcoderApp.jar createdb

This creates the cloudcoder database, as well as your initial cloudcoder user account.  Note that the database should not already exist, but the mysql account should have sufficient permissions to create it.  You will be prompted for the cloudcoder username and password you would like to use; you will use this username/password to log into the cloudcoder server and it does not need to match the mysql username or any other username.  Be sure to use the default value for the exercise repository (`https://cloudcoder.org/repo`).

List your configuration properties, and make sure they match what you put in your cloudcoder.properties.

	java -jar cloudcoderApp.jar listconfig

### Create a new course

Create a new course:

	java -jar cloudcoderApp.jar createcourse

Then follow the prompts
