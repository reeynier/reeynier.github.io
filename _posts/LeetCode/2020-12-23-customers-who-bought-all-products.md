---
layout: post
title:  "Customers Who Bought All Products Problem"
categories: [ Database ]
tags: [ MySQL, Leetcode ]
similar: [ DatabaseGroup8 ]
featured: false
hidden: false
sidenav: LeetcodeDatabaseMedium1
excerpt: LeetCode 1045. Write an SQL query for a report that provides the customer ids from the Customer table that bought all the products in the Product table.

---

<br />

## Description

LeetCode Problem 1045. 

Table: Customer

```
+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| customer_id | int     |
| product_key | int     |
+-------------+---------+
product_key is a foreign key to Product table.
```

Table: Product

```
+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| product_key | int     |
+-------------+---------+
product_key is the primary key column for this table.
```

Write an SQL query for a report that provides the customer ids from the Customer table that bought all the products in the Product table.

Return the result table in any order.

The query result format is in the following example:
 
```
Customer table:
+-------------+-------------+
| customer_id | product_key |
+-------------+-------------+
| 1           | 5           |
| 2           | 6           |
| 3           | 5           |
| 3           | 6           |
| 1           | 6           |
+-------------+-------------+

Product table:
+-------------+
| product_key |
+-------------+
| 5           |
| 6           |
+-------------+

Result table:
+-------------+
| customer_id |
+-------------+
| 1           |
| 3           |
+-------------+
The customers who bought all the products (5 and 6) are customers with id 1 and 3.
```

<br />

## MySQL Solution


```sql
select customer_id
from Customer
group by customer_id
having count(distinct product_key) = 
    (select count(distinct product_key) from Product)
```
