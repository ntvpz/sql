---
layout: post
title: “MySQL server has gone away“ - Why and how to fix?
description: MySQL server dies halfway through processing big files with the following error “MySQL server has gone away“. What to do?
summary: MySQL server dies halfway through processing big files with the following error “MySQL server has gone away“. What to do?
tags: mysql networking
minute: 2
---

While running a large operation such as importing a big SQL dump file, MySQL might die halfway through with the following error:

> “General error: 2006 MySQL server has gone away“

It can also be one of these:

> Error Code: 2013. Lost connection to MySQL server during query

> Warning: Error while sending QUERY packet

> PDOException: SQLSTATE[HY000]: General error: 2006 MySQL server has gone away


There are two reasons for that error:

* The server timed out and closed the connection.
* The server dropped a too large packet. If `mysqld` receives a packet that is too large, it assumes that something has gone wrong with the client and closes the connection.

**Here's what happened**: You and MySQL server were doing some business and you gave it a relatively large deal. MySQL didn't say no, it carried on with the task. After running for a while, MySQL changed its mind and said: "The task is either too big or taking too long, so I'm out of this shit". 

Then it timed out and closed the connection.

You can try the 2 methods below to fix it:

### 1. Increase the `wait_timeout`

First, check the current `wait_timeout` value:

```
SELECT @@wait_timeout;
```

Then set a higher value for `wait_timeout`:

```
SET GLOBAL wait_timeout=600;
```

Where `600` is the number of seconds you need for the queries to take up to.

You can also go to your `my.cnf` configuration file (Can be found in `/etc/mysql/my.cnf`) and set the `wait_timeout` variable.

Then restart the server and try again.

### 2. Increate the `max_allowed_packet` variable

This value by default is small and normally is the cause.

First, check the current `max_allowed_packet` value:

```
SELECT @@max_allowed_packet;
```

Then set a bigger `max_allowed_packet` value:

```
SET GLOBAL max_allowed_packet=107374182;
```

You can set your own value, `107374182` is equivalent to 100MB.

You can also access and edit the `max_allowed_packet` variable inside the MySQL configuration file `my.cnf`:

```
max_allowed_packet=107374182
```

Then restart the server and try again.

In some other cases, it's just because the MySQL server has run out of RAM, so you might need to check that as well.
