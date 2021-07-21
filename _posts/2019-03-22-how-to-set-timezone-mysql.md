---
layout: post
title: How to set timezone in MySQL?
description: 3 ways to configure timezone in MySQL
summary: 3 ways to configure timezone in MySQL
tags: mysql
minute: 1
---


There are 3 ways to set timezone in MySQL

* Using MySQL configuration file `my.cnf`
* Using `@@global.time_zone` variable
* Using `@@session.time_zone` variable

Let's get into each of them.

### 1. Set timezone using the file `my.cnf`

Go to your MySQL configuration fire `my.cnf`, usually found in `/etc/mysql/my.cnf`, you can see the `default-time-zone` variable in the `[mysqld]` section. Then set it to the timezone you want:

```
default-time-zone='timezone'
```

### 2. Set timezone using the `@@global.time_zone` variable

To see the current timezone value:

```
SELECT @@global.time_zone;
```

Set it to the timezone you want:

```
SET @@global.time_zone = 'timezone';
```

You can also use the following query:

```
SET GLOBAL time_zone = 'timezone';
```

### 3. Set timezone using the `@@session.time_zone` variable

It's quite similar to the `@@global.time_zone` variable.

To see the current timezone value:

```
SELECT @@session.time_zone;
```

Set it to the timezone you want:

```
SET @@session.time_zone = 'timezone';
```

You can also use the following query:

```
SET time_zone = 'timezone';
```

For more detailed information, please see the [MySQL documentation](https://dev.mysql.com/doc/refman/8.0/en/time-zone-support.html)
