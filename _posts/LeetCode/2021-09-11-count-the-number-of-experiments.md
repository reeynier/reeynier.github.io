---
layout: post
title:  "Count the Number of Experiments Problem"
categories: [ Database ]
tags: [ MySQL, Leetcode ]
similar: [ DatabaseGroup30 ]
featured: false
hidden: false
sidenav: LeetcodeDatabaseMedium4
excerpt: LeetCode 1990. Write an SQL query to report the number of experiments done on each of the three platforms for each of the three given experiments. 
---

<br />

## Description

LeetCode Problem 1990. 

Table: Experiments
```
+-----------------+------+
| Column Name     | Type |
+-----------------+------+
| experiment_id   | int  |
| platform        | enum |
| experiment_name | enum |
+-----------------+------+
experiment_id is the primary key for this table.
platform is an enum with one of the values ('Android', 'IOS', 'Web').
experiment_name is an enum with one of the values ('Reading', 'Sports', 'Programming').
This table contains information about the ID of an experiment done with a random person, the platform used to do the experiment, and the name of the experiment.
```
 

Write an SQL query to report the number of experiments done on each of the three platforms for each of the three given experiments. Notice that all the pairs of (platform, experiment) should be included in the output including the pairs with zero experiments.

Return the result table in any order.

The query result format is in the following example.

 

Example 1:
```
Input:
Experiments table:
+---------------+----------+-----------------+
| experiment_id | platform | experiment_name |
+---------------+----------+-----------------+
| 4             | IOS      | Programming     |
| 13            | IOS      | Sports          |
| 14            | Android  | Reading         |
| 8             | Web      | Reading         |
| 12            | Web      | Reading         |
| 18            | Web      | Programming     |
+---------------+----------+-----------------+
Output: 
+----------+-----------------+-----------------+
| platform | experiment_name | num_experiments |
+----------+-----------------+-----------------+
| Android  | Reading         | 1               |
| Android  | Sports          | 0               |
| Android  | Programming     | 0               |
| IOS      | Reading         | 0               |
| IOS      | Sports          | 1               |
| IOS      | Programming     | 1               |
| Web      | Reading         | 2               |
| Web      | Sports          | 0               |
| Web      | Programming     | 1               |
+----------+-----------------+-----------------+
Explanation: 
On the platform "Android", we had only one "Reading" experiment.
On the platform "IOS", we had one "Sports" experiment and one "Programming" experiment.
On the platform "Web", we had two "Reading" experiments and one "Programming" experiment.
```

<br />

## MySQL Solution


```sql
select 
    platform, 
    experiment_name, 
    ifnull(num_experiments, 0) as num_experiments
from 
    (select "Android" as platform
     union
     select "IOS" as platform
     union
     select "Web" as platform) a 
    cross join (select "Reading" as experiment_name
                union 
                select "Sports" as experiment_name
                union
                select "Programming" as experiment_name) b
    left join (select platform, experiment_name, count(*) as num_experiments 
               from Experiments 
               group by 1, 2) c
    using (platform, experiment_name)
order by 1, 2
```
