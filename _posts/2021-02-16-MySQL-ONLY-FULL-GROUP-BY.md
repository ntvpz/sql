---
layout: post
title: MySQL's ONLY_FULL_GROUP_BY mode - How to disable it?
description: MySQL's ONLY_FULL_GROUP_BY mode - How to disable it?
summary: MySQL's ONLY_FULL_GROUP_BY mode - How to disable it?
tags: mysql
minute: 1
---

If you run into this error with MySQL:

> Expression #1 of SELECT list is not in GROUP BY clause and contains nonaggregated column 'db.table.col' which is not functionally dependent on columns in GROUP BY clause; this is incompatible with sql_mode=only_full_group_by

It’s likely because you have the ONLY_FULL_GROUP_BY function enabled. To fix this, you have to disable it.

First, check the current `sql_mode`:

```
SELECT @@sql_mode;
```

The result would include `ONLY_FULL_GROUP_BY`:

```
ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION
```

Then copy the current `sql_mode` values from the result, remove `ONLY_FULL_GROUP_BY`, find and edit `my.cnf` (Usually found in /etc/my.cnf or /etc/mysql/my.cnf.) and put it under `[mysqld]` section:

```
sql_mode=STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION
```

Then restart the mysql server.

An alternative to remove `ONLY_FULL_GROUP_BY` without touching any other setting:

```
SET GLOBAL sql_mode=(SELECT REPLACE(@@sql_mode,'ONLY_FULL_GROUP_BY',''));
```

