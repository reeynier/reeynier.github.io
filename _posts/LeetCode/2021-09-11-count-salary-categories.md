---
layout: post
title:  "Count Salary Categories Problem"
categories: [ Database ]
tags: [ MySQL, Leetcode ]
similar: [ DatabaseGroup28 ]
featured: false
hidden: false
sidenav: LeetcodeDatabaseMedium4
excerpt: LeetCode 1907. Write an SQL query to report the number of bank accounts of each salary category.
---

<br />

## Description

LeetCode Problem 1907. 

Table: Accounts
```
+-------------+------+
| Column Name | Type |
+-------------+------+
| account_id  | int  |
| income      | int  |
+-------------+------+
account_id is the primary key for this table.
Each row contains information about the monthly income for one bank account.
```

Write an SQL query to report the number of bank accounts of each salary category. The salary categories are:

* "Low Salary": All the salaries strictly less than $20000.
* "Average Salary": All the salaries in the inclusive range [$20000, $50000].
* "High Salary": All the salaries strictly greater than $50000.

The result table must contain all three categories. If there are no accounts in a category, then report 0. Return the result table in any order.

The query result format is in the following example.

 
```
Accounts table:
+------------+--------+
| account_id | income |
+------------+--------+
| 3          | 108939 |
| 2          | 12747  |
| 8          | 87709  |
| 6          | 91796  |
+------------+--------+

Result table:
+----------------+----------------+
| category       | accounts_count |
+----------------+----------------+
| Low Salary     | 1              |
| Average Salary | 0              |
| High Salary    | 3              |
+----------------+----------------+

Low Salary: Account 2.
Average Salary: No accounts.
High Salary: Accounts 3, 6, and 8.
```

<br />

## MySQL Solution


```sql
select "Low Salary" as category, count(*) as accounts_count from Accounts where income < 20000
union 
select "Average Salary" as category, count(*) as accounts_count from Accounts where 20000 <= income and income <= 50000
union
select "High Salary" as category, count(*) as accounts_count from Accounts where 50000 < income
```
