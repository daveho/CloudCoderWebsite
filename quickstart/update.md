---
layout: default
title: How to update CloudCoder
---
[Prev](commands.html) | Next

### Updating CloudCoder

We may distribute new pre-compiled CloudCoder binaries (bug fixes, new features, etc).  To take advantage of these new binaries:

1. Download the new binaries and put them into a new folder.  Do not copy over your existing cloudcoder binaries, in case the new distribution has an error (hopefully unlikely since the CloudCoder team are awesome coders, but certainly possible).

2. Copy your existing cloudcoder.properties file into the folder containing your new binaries.

3. [Configure the CloudCoder binaries](configure.html) following the same steps outlined previously in this quickstart guide.

4. Shutdown your current CloudCoder builders ([instructions here](builder.html))

5. Shutdown your current CloudCoder server ([instructions here](commands.html))

6. Start the new server in a new folder.  Since it will use the same CloudCoder database, it should work without any configuration on the database.

7. Start the new builders.
