---
layout: post
title:  "Customers Who Never Order Problem"
categories: [ Database ]
tags: [ MySQL, Leetcode ]
similar: [ DatabaseGroup2 ]
featured: false
hidden: false
excerpt: LeetCode 183. Write a SQL query to find all customers who never order anything.
---

<br />

## Description

LeetCode Problem 183. 

Suppose that a website contains two tables, the Customers table and the Orders table. Write a SQL query to find all customers who never order anything.

Table: Customers.

```
+----+-------+
| Id | Name  |
+----+-------+
| 1  | Joe   |
| 2  | Henry |
| 3  | Sam   |
| 4  | Max   |
+----+-------+
```

Table: Orders.

```
+----+------------+
| Id | CustomerId |
+----+------------+
| 1  | 3          |
| 2  | 1          |
+----+------------+
```

Using the above tables as example, return the following:

```
+-----------+
| Customers |
+-----------+
| Henry     |
| Max       |
+-----------+
```

<br />

## MySQL Solution


```sql
select c.Name as Customers
from Customers c
where c.Id not in (select CustomerId from Orders)
```
