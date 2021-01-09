---
layout: post
title:  "Winning Candidate Problem"
categories: [ Database ]
tags: [ MySQL, Leetcode ]
similar: [ DatabaseGroup4 ]
featured: false
hidden: false
sidenav: LeetcodeDatabaseMedium1
excerpt: LeetCode 574. Write a sql to find the name of the winning candidate, the above example will return the winner B.
---

<br />

## Description

LeetCode Problem 574. 

Table: Candidate

```
+-----+---------+
| id  | Name    |
+-----+---------+
| 1   | A       |
| 2   | B       |
| 3   | C       |
| 4   | D       |
| 5   | E       |
+-----+---------+  
```

Table: Vote

```
+-----+--------------+
| id  | CandidateId  |
+-----+--------------+
| 1   |     2        |
| 2   |     4        |
| 3   |     3        |
| 4   |     2        |
| 5   |     5        |
+-----+--------------+
id is the auto-increment primary key,
CandidateId is the id appeared in Candidate table.
```

Write a sql to find the name of the winning candidate, the above example will return the winner B.

```
+------+
| Name |
+------+
| B    |
+------+
```

Notes: You may assume there is no tie, in other words there will be only one winning candidate.

<br />

## MySQL Solution


```sql
select name as 'Name'
from Candidate
join (select Candidateid
    from Vote
    group by Candidateid
    order by count(*) desc
    limit 1) as winner
where Candidate.id = winner.Candidateid
```
