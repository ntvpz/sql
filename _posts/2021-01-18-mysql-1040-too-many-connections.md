---
layout: post
title: 1040 “Too many connections” & Increase max connections in MySQL
description: 1040 “Too many connections” & Increase max connections in MySQL
summary: 1040 “Too many connections” & Increase max connections in MySQL
tags: mysql
minute: 1
---

When you reached the maximum number of connections to the MySQL Server, your connection attempts will get rejected by the server with the following error:

> MySQL: ERROR 1040: Too many connections

The maximum number of connections is defined in the `max_connections` variable. To allow more connections simultaneously, you need to set a higher value for `max_connections`.

To see the current value of `max_connections`:

```
SHOW VARIABLES LIKE "max_connections";
```

The result should be like this:

+-----------------+-------+
| Variable_name   | Value |
+-----------------+-------+
| max_connections | 100   |
+-----------------+-------+

MySQL actually allows up to max_connections + 1 connections as the extra connection can be used by the user with `CONNECTION_ADMIN` privilege only.

Now set a higher value for `max_connections`:

```
SET GLOBAL max_connections = 500;
```

You can also increase it by editing the configuration file [my.cnf](https://randomsql.com/2020/05/where-to-find-mysql-mycnf-file)

Under the [mysqld] section add the following line:

```
max_connections = 500
```

Then restart the MySQL server to take effect.

See the [official docs](https://dev.mysql.com/doc/refman/8.0/en/too-many-connections.html) from MySQL for more information.
