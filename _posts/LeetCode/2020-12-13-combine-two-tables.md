---
layout: post
title:  "Combine Two Tables Problem"
categories: [ Database ]
tags: [ MySQL, Leetcode ]
similar: [ DatabaseGroup1 ]
featured: false
hidden: false
excerpt: LeetCode 175. Write a SQL query for a report that provides the following information for each person in the Person table,
---

<br />

## Description

LeetCode Problem 175. 

Table: Person

```
+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| PersonId    | int     |
| FirstName   | varchar |
| LastName    | varchar |
+-------------+---------+
PersonId is the primary key column for this table.
```

Table: Address

```
+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| AddressId   | int     |
| PersonId    | int     |
| City        | varchar |
| State       | varchar |
+-------------+---------+
AddressId is the primary key column for this table.
``` 

Write a SQL query for a report that provides the following information for each person in the Person table, regardless if there is an address for each of those people:

```
FirstName, LastName, City, State
```


<br />

## MySQL Solution

We can join the two tables to get the address information of a person. Considering there might not be an address information for every person, we should use outer join instead of the default inner join.

```sql
select Person.FirstName, Person.LastName, Address.City, Address.State
from Person
left join Address on Person.PersonId = Address.PersonId;
```
