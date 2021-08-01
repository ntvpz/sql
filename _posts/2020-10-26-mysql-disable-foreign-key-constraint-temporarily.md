---
layout: post
title: MySQL - How to disable a foreign key constraint temporarily?
description: How can I temporarily disable a foreign key constraint in MySQL?
summary: How can I temporarily disable a foreign key constraint in MySQL?
tags: mysql
minute: 1
---

In some cases, altering a table that has foreign key constraints would be troublesome, especially if you have a lot of tables with parent-child relationship. So it's really helpful to disable foreign key constraint checks in MySQL. Here's how.

### 1. You can disable foreign key check in MySQL by setting the system variable `foreign_key_checks` to 0

```
SET FOREIGN_KEY_CHECKS=0;
```

It's just that simple. And when you need to turn it back on, simple set it to 1:

```
SET FOREIGN_KEY_CHECKS=1;
```

Please be noted that it only appy to the current connection, so if you want to disable it for all connections, use the follow query:

```
SET GLOBAL FOREIGN_KEY_CHECKS=0;
```

Similarly, enable it when you're done:

```
SET GLOBAL FOREIGN_KEY_CHECKS=1;
```

### 2. You can also disable foreign key check using `DISABLE KEYS`

Like this:

```
ALTER TABLE table_name DISABLE KEYS;
```

And to turn it back on after that:

```
ALTER TABLE table_name ENABLE KEYS;
```

*Note that DISABLE KEYS does not work on InnoDB tables as it works properly for MyISAM.*

### 3. A little trick, use `ON DELETE SET NULL`

Instead of turning foreign key check on and off which might cause unwanted data integrity issue, you can use `ON DELETE SET NULL` on the target table:

Alter the table and delete the current foreign key first:

```
ALTER TABLE table_name1 DROP FOREIGN KEY fk_name1; 
ALTER TABLE table_name2 DROP FOREIGN KEY fk_name2;
```

Then add the foreign key constraints back

```
ALTER TABLE table_name1 
  ADD FOREIGN KEY (table2_id) 
        REFERENCES table2(id)
        ON DELETE SET NULL;

ALTER TABLE tablename2 
  ADD FOREIGN KEY (table1_id) 
        REFERENCES table1(id)
        ON DELETE SET NULL;
```
