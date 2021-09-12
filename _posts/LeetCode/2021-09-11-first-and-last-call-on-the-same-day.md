---
layout: post
title:  "First and Last Call On the Same Day Problem"
categories: [ Database ]
tags: [ MySQL, Leetcode ]
similar: [ DatabaseGroup30 ]
featured: false
hidden: false
sidenav: LeetcodeDatabaseHard1
excerpt: LeetCode 1972. Write an SQL query to report the IDs of the users whose first and last calls on any day were with the same person.
---

<br />

## Description

LeetCode Problem 1972. 

Table: Calls
```
+--------------+----------+
| Column Name  | Type     |
+--------------+----------+
| caller_id    | int      |
| recipient_id | int      |
| call_time    | datetime |
+--------------+----------+
(caller_id, recipient_id, call_time) is the primary key for this table.
Each row contains information about the time of a phone call between caller_id and recipient_id.
```

Write an SQL query to report the IDs of the users whose first and last calls on any day were with the same person. Calls are counted regardless of being the caller or the recipient.

Return the result table in any order.

The query result format is in the following example:

 
```
Calls table:
+-----------+--------------+---------------------+
| caller_id | recipient_id | call_time           |
+-----------+--------------+---------------------+
| 8         | 4            | 2021-08-24 17:46:07 |
| 4         | 8            | 2021-08-24 19:57:13 |
| 5         | 1            | 2021-08-11 05:28:44 |
| 8         | 3            | 2021-08-17 04:04:15 |
| 11        | 3            | 2021-08-17 13:07:00 |
| 8         | 11           | 2021-08-17 22:22:22 |
+-----------+--------------+---------------------+

Result table:
+---------+
| user_id |
+---------+
| 1       |
| 4       |
| 5       |
| 8       |
+---------+

On 2021-08-24, the first and last call of this day for user 8 was with user 4. User 8 should be included in the answer.
Similary, user 4 on 2021-08-24 had their first and last call with user 8. User 4 should be included in the answer.
On 2021-08-11, user 1 and 5 had a call. This call was the only call for both of them on this day. Since this call is the first and last call of the day for both of them, they should both be included in the answer.
```


<br />

## MySQL Solution


```sql
with A as(
    select caller_id as id1, recipient_id as id2, right(call_time, 8) as call_time, left(call_time, 10) as call_day from Calls
    union all 
    select recipient_id as id1, caller_id as id2, right(call_time, 8) as call_time, left(call_time, 10) as call_day from Calls
),
B as(
    select id1, id2, call_day,
    rank() over(partition by id1, call_day order by call_time) as rnk1,
    rank() over(partition by id1, call_day order by call_time desc) as rnk2
    from A 
),
C as(
    select distinct B1.id1 as user_id from B B1 inner join B B2 on B1.id1=B2.id1 and B1.id2=B2.id2 and B1.call_day=B2.call_day where B1.rnk1=1 and B2.rnk2=1 
)
select * from C
```
