---
layout: post
title:  "Students Report By Geography Problem"
categories: [ Database ]
tags: [ MySQL, Leetcode ]
similar: [ DatabaseGroup7 ]
featured: false
hidden: false
sidenav: LeetcodeDatabaseHard1
excerpt: LeetCode 618. A U.S graduate school has students from Asia, Europe and America. 
---

<br />

## Description

LeetCode Problem 618. 

A U.S graduate school has students from Asia, Europe and America. The students' location information are stored in table student as below.
 
```
| name   | continent |
|--------|-----------|
| Jack   | America   |
| Pascal | Europe    |
| Xi     | Asia      |
| Jane   | America   |
```

Pivot the continent column in this table so that each name is sorted alphabetically and displayed underneath its corresponding continent. The output headers should be America, Asia and Europe respectively. It is guaranteed that the student number from America is no less than either Asia or Europe.
 

For the sample input, the output is:
 
```
| America | Asia | Europe |
|---------|------|--------|
| Jack    | Xi   | Pascal |
| Jane    |      |        |
```

<br />

## MySQL Solution


```sql
select America, Asia, Europe
from 
    (select name as America, row_number() over () as rn
    from student
    where continent = 'America'
    order by America) a
left join     
    (select name as Asia, row_number() over () as tn
    from student
    where continent = 'Asia'
    order by Asia)  b
on rn = tn    
left join
    (select name as Europe, row_number() over () as kn
    from student
    where continent = 'Europe'
    order by Europe)  c    
on rn = kn
```
