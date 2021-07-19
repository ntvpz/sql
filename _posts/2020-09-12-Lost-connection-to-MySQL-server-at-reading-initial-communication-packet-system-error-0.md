---
layout: post
title: Lost connection to MySQL server at 'reading initial communication packet', system error 0
description: MySQL error Lost connection to MySQL server at 'reading initial communication packet', system error 0 and how to fix it
summary: MySQL error Lost connection to MySQL server at 'reading initial communication packet', system error 0 and how to fix it
tags: mysql networking
minute: 1
---


You might run into this error while trying to connect to a MySQL database:

> "Lost connection to MySQL server at 'reading initial communication packet, system error: 0"

This is somewhat confusing because error 0 means success.

In most cases, there's a problem with the firewall blocking outside connection. The first thing to do is to check the firewall rules and see if the MySQL connection request is blocked. If yes, then approve and it's good to go.

If the firewall is not the issue, the next thing to check is the `bind-address` variable in the my.cnf file (can be found at /etc/mysql/my.cnf). By default it binds to localhost so connections from others addresses will be ignored.

Open the my.cnf file and comment out the bind address line, you can find it under the [mysqld] section:

```
#bind-address = 127.0.0.1
```

You can also bind to all available IP addresses instead. If so, just use 0.0.0.0 for a binding address.

Then restart the MySQL server:

```
sudo service mysql restart
```

If that's still not the cause, there are a few other things to take a look at:

* Check the MySQL listening port. 3306 is the default, but this can be changed.

* Check the user's rights to connect to the server IP from your address.

* Make sure you are both providing a password if needed and using the correct password for connecting from the host address you’re connecting from

