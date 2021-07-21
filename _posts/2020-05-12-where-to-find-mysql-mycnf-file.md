---
layout: post
title: Can't find my.cnf file - Where is the MySQL my.cnf location?
description: Where is the MySQL my.cnf location? How to find it?
summary: Where is the MySQL my.cnf location? How to find it?
tags: mysql
minute: 1
---

If you work with MySQL long enough, you will find yourself going into this MySQL configuration file again and again. However, its location is a bit tricky.

There are 2 common default locations that you can see your my.cnf file:

* `/etc/my.cnf`
* `/etc/mysql/my.cnf`

You can also look for these:

* `$MYSQL_HOME/my.cnf`
* `[datadir]/my.cnf`
* `~/.my.cnf`

If you still can't find it, this command might help:

```
mysql --help
```

It will show you something like this:

```
Default options are read from the following files in the given order: /etc/mysql/my.cnf /etc/my.cnf ~/.my.cnf
...
```

From what is printed, you can see the location of your configuration file.

For more detailed information, please see the [MySQL documentation](https://dev.mysql.com/doc/refman/8.0/en/option-files.html)
