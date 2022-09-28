---
layout: post
title:  "How To Output MySQL Query Results In CSV Format"
categories: [ MySQL ]
tags: [ Database, Query, MySQL ]
similar: [ MySQL Common Query ]
featured: false
hidden: false
sidenav: MySQL
excerpt: This query writes results into a CSV file on the server that is running MySQL.
---

<br />

## Short Answer

```sql
SELECT *
INTO OUTFILE '/tmp/results.csv'
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
FROM TABLE
```

This query writes results into a CSV file on the server that is running MySQL. Column names will not be exported. 

Each field will be encouled in double quotes, the fields will be separated by commas, and each row will be output on a new line separated by \n. Sample output of this query would look like: 

```
"1","Clark","Sales"
"2","Dave","Accounting"
"3","Ava","Sales"
```





