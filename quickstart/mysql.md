---
layout: default
title: Configure MySQL
---
Prev | [Next](configure.html)

### Configuring MySQL

You will need to create a MySQL user for the CloudCoder webapp
to use.  The username `cloudcoder` is a good choice.  To create the user,
run the command

	mysql --user=root --pass \
	--execute="create user 'cloudcoder'@'localhost' identified by 'somepassword'"

Enter the password for the MySQL `root` user when prompted.
Replace `somepassword` with the password you
want to use.  (If you chose a different username, replace
`cloudcoder` with that username.)

Next, grant the cloudcoder user account permission to create the database:

	mysql --user=root --pass \
	--execute="grant all on cloudcoderdb.* to 'cloudcoder'@'localhost'"

Again, replace `cloudcoder` and `cloudcoderdb` with the username and
database name you chose previously.

