---
layout: post
title: MySQL - How to generate the query log to show executed queries?
description: MySQL - How to generate the query log to show executed queries?
summary: MySQL - How to generate the query log to show executed queries?
tags: mysql
minute: 1
---

There's a way to trace MySQL queries as they are executed on the server.

### 1. First, enable query logging on the database:

```
SET GLOBAL log_output = "TABLE";
SET GLOBAL general_log = 1;
```

### 2. Now you can view the log from the table `mysql.general_log`:

```
SELECT
    *
FROM
    mysql.general_log;
```

If you want to log the output to a file instead:

```
SET GLOBAL log_output = "FILE";
SET GLOBAL general_log_file = "/path/to/your/logfile.log"
SET GLOBAL general_log = 1;
```

### 3. When you want to disable query logging:

```
SET GLOBAL general_log = 0;
```

See the [official docs](https://dev.mysql.com/doc/refman/8.0/en/query-log.html) from MySQL for more information about the General Query Log.
