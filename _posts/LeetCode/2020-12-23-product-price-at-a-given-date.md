---
layout: post
title:  "Product Price At A Given Date Problem"
categories: [ Database ]
tags: [ MySQL, Leetcode ]
similar: [ DatabaseGroup13 ]
featured: false
hidden: false
sidenav: LeetcodeDatabaseMedium2
excerpt: LeetCode 1164. Write an SQL query to find the prices of all products on 2019-08-16.
---

<br />

## Description

LeetCode Problem 1164. 

Table: Products

```
+---------------+---------+
| Column Name   | Type    |
+---------------+---------+
| product_id    | int     |
| new_price     | int     |
| change_date   | date    |
+---------------+---------+
(product_id, change_date) is the primary key of this table.
Each row of this table indicates that the price of some product was changed to a new price at some date.
```

Write an SQL query to find the prices of all products on 2019-08-16. Assume the price of all products before any change is 10.

The query result format is in the following example:

```
Products table:
+------------+-----------+-------------+
| product_id | new_price | change_date |
+------------+-----------+-------------+
| 1          | 20        | 2019-08-14  |
| 2          | 50        | 2019-08-14  |
| 1          | 30        | 2019-08-15  |
| 1          | 35        | 2019-08-16  |
| 2          | 65        | 2019-08-17  |
| 3          | 20        | 2019-08-18  |
+------------+-----------+-------------+

Result table:
+------------+-------+
| product_id | price |
+------------+-------+
| 2          | 50    |
| 1          | 35    |
| 3          | 10    |
+------------+-------+
```

<br />

## MySQL Solution


```sql
select p1.product_id, p1.new_price as price
from Products p1
where p1.change_date <= '2019-08-16' and
    (product_id, datediff('2019-08-16', p1.change_date)) in
    (select product_id, min(datediff('2019-08-16', change_date))
    from Products
    where change_date <= '2019-08-16'
    group by product_id)

union

select product_id, 10 as price
from Products
group by product_id
having min(change_date) > '2019-08-16'
order by price desc
```
