---
layout: post
title:  "Consecutive Available Seats Problem"
categories: [ Database ]
tags: [ MySQL, Leetcode ]
similar: [ DatabaseGroup6 ]
featured: false
hidden: false
excerpt: LeetCode 603. Several friends at a cinema ticket office would like to reserve consecutive available seats.
---

<br />

## Description

LeetCode Problem 603. 

Several friends at a cinema ticket office would like to reserve consecutive available seats.
Can you help to query all the consecutive available seats order by the seat_id using the following cinema table?

```
| seat_id | free |
|---------|------|
| 1       | 1    |
| 2       | 0    |
| 3       | 1    |
| 4       | 1    |
| 5       | 1    |
```

Your query should return the following result for the sample case above.
 
```
| seat_id |
|---------|
| 3       |
| 4       |
| 5       |
```

Note:
* The seat_id is an auto increment int, and free is bool ('1' means free, and '0' means occupied.).
* Consecutive available seats are more than 2(inclusive) seats consecutively available.

<br />

## MySQL Solution


```sql
select c1.seat_id
from cinema c1, cinema c2
where ((c1.seat_id = c2.seat_id+1) or
       (c1.seat_id = c2.seat_id-1)) and 
    (c1.free = 1) and (c2.free = 1)
group by c1.seat_id
```
