---
layout: post
title:  "Total Sales Amount By Year Problem"
categories: [ Database ]
tags: [ MySQL, Leetcode ]
similar: [ DatabaseGroup18 ]
featured: false
hidden: false
sidenav: LeetcodeDatabaseHard1
excerpt: LeetCode 1384. Write an SQL query to report the Total sales amount of each item for each year, with corresponding product name, product_id, product_name and report_year.
---

<br />

## Description

LeetCode Problem 1384. 

Table: Product

```
+---------------+---------+
| Column Name   | Type    |
+---------------+---------+
| product_id    | int     |
| product_name  | varchar |
+---------------+---------+
product_id is the primary key for this table.
product_name is the name of the product.
```

Table: Sales

```
+---------------------+---------+
| Column Name         | Type    |
+---------------------+---------+
| product_id          | int     |
| period_start        | date    |
| period_end          | date    |
| average_daily_sales | int     |
+---------------------+---------+
product_id is the primary key for this table. 
period_start and period_end indicates the start and end date for sales period, both dates are inclusive.
The average_daily_sales column holds the average daily sales amount of the items for the period.
```

Write an SQL query to report the Total sales amount of each item for each year, with corresponding product name, product_id, product_name and report_year.

Dates of the sales years are between 2018 to 2020. Return the result table ordered by product_id and report_year.

The query result format is in the following example:

```
Product table:
+------------+--------------+
| product_id | product_name |
+------------+--------------+
| 1          | LC Phone     |
| 2          | LC T-Shirt   |
| 3          | LC Keychain  |
+------------+--------------+

Sales table:
+------------+--------------+-------------+---------------------+
| product_id | period_start | period_end  | average_daily_sales |
+------------+--------------+-------------+---------------------+
| 1          | 2019-01-25   | 2019-02-28  | 100                 |
| 2          | 2018-12-01   | 2020-01-01  | 10                  |
| 3          | 2019-12-01   | 2020-01-31  | 1                   |
+------------+--------------+-------------+---------------------+

Result table:
+------------+--------------+-------------+--------------+
| product_id | product_name | report_year | total_amount |
+------------+--------------+-------------+--------------+
| 1          | LC Phone     |    2019     | 3500         |
| 2          | LC T-Shirt   |    2018     | 310          |
| 2          | LC T-Shirt   |    2019     | 3650         |
| 2          | LC T-Shirt   |    2020     | 10           |
| 3          | LC Keychain  |    2019     | 31           |
| 3          | LC Keychain  |    2020     | 31           |
+------------+--------------+-------------+--------------+
LC Phone was sold for the period of 2019-01-25 to 2019-02-28, and there are 35 days for this period. Total amount 35*100 = 3500. 
LC T-shirt was sold for the period of 2018-12-01 to 2020-01-01, and there are 31, 365, 1 days for years 2018, 2019 and 2020 respectively.
LC Keychain was sold for the period of 2019-12-01 to 2020-01-31, and there are 31, 31 days for years 2019 and 2020 respectively.
```

<br />

## MySQL Solution


```sql
select *
from (

        select s.product_id, product_name, '2018' as report_year, 
               case when year(period_end) = 2018 then average_daily_sales * (dayofyear(period_end)-dayofyear(period_start) + 1)
                    when year(period_end) >= 2019 then average_daily_sales * (365 - dayofyear(period_start) + 1)
                    end as total_amount
        from Sales s left join Product p on s.product_id = p.product_id
        where year(period_start) = 2018

        union

        select s.product_id, product_name,'2019' as report_year, 
               case when year(period_start) = 2018 and year(period_end) = 2019 then average_daily_sales * dayofyear(period_end)
                    when year(period_start)=2018 and year(period_end) = 2020 then average_daily_sales * 365
                    when year(period_start) = 2019 and year(period_end) = 2019 then average_daily_sales * (dayofyear(period_end) - dayofyear(period_start) + 1)
                    when year(period_start) = 2019 and year(period_end) = 2020 then average_daily_sales * (365 - dayofyear(period_start) + 1)
                    end as total_amount
        from Sales s left join Product p on s.product_id = p.product_id
        where year(period_start) < 2020 and year(period_end) > 2018

        union

        select s.product_id, product_name,'2020' as report_year, 
               case when year(period_start) < 2020 then average_daily_sales * dayofyear(period_end)
                    when year(period_start) = 2020 then average_daily_sales * (dayofyear(period_end) - dayofyear(period_start) + 1)
                    end as total_amount
        from Sales s left join Product p on s.product_id = p.product_id
        where year(period_end) = 2020
) a
order by product_id, report_year
```
