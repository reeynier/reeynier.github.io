---
layout: post
title:  "How To Get A List Of User Accounts In MySQL"
categories: [ MySQL ]
tags: [ Database, Query, MySQL ]
similar: [ MySQL Common Query ]
featured: false
hidden: false
sidenav: MySQL
excerpt: MySQL stores the user information in its own database.
---

<br />

## Short Answer

```sql
SELECT DISTINCT User FROM mysql.user;
```

MySQL stores the user information in its own database. The name of the database is mysql. Inside that database, the user information is in a table named user. This query gets unique user accounts. Sample output of this query would look like: 

```
+-------+
| User  |
+-------+
| root  |
+-------+
| user2 |
+-------+
```





