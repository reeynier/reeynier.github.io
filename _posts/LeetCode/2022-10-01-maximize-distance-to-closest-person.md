---
layout: post
title: "Maximize Distance To Closest Person Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array ]
similar: [ Array ]
featured: false
hidden: false
excerpt: LeetCode 849. You are given an array representing a row of seats where seats[i] = 1 represents a person sitting in the i^th seat, and seats[i] = 0 represents that the i^th seat is empty (0-indexed).

---

<br />

## Description

LeetCode Problem 849.

You are given an array representing a row of seats where seats[i] = 1 represents a person sitting in the i^th seat, and seats[i] = 0 represents that the i^th seat is empty (0-indexed).

There is at least one empty seat, and at least one person sitting.

Alex wants to sit in the seat such that the distance between him and the closest person to him is maximized.

Return that maximum distance to the closest person.

Example 1: 
```
Input: seats = [1,0,0,0,1,0,1]
Output: 2
Explanation: 
If Alex sits in the second open seat (i.e. seats[2]), then the closest person has distance 2.
If Alex sits in any other open seat, the closest person has distance 1.
Thus, the maximum distance to the closest person is 2.
```

Example 2:
```
Input: seats = [1,0,0,0]
Output: 3
Explanation: 
If Alex sits in the last seat (i.e. seats[3]), the closest person is 3 seats away.
This is the maximum distance possible, so the answer is 3.
```

Example 3:
```
Input: seats = [0,1]
Output: 1
```

Constraints:
* 2 <= seats.length <= 2 * 10^4
* seats[i]is 0 or1.
* At least one seat is empty.
* At least one seat is occupied.

<br />

## Sample C++ Code


```c
class Solution {
public:
    int maxDistToClosest(vector<int>& seats) {
        int longest = 0, beginning = 0, i = 0;
        
        // count zeros in beginning
        while (seats[i] == 0) {
            beginning++;
            i++;
        }
        
        // find longest sequence of zeros in middle
        int count = beginning;
        for (; i < seats.size(); i++) {
            if (seats[i] == 0)
                count++;
            else {
                longest = std::max({count, longest});
                count = 0;
            }
        }
        
        // at the end, count = length of zeros in the end
        // in the middle we have to divide the length in two to find maximum distance
        longest = longest%2 == 0 ? longest/2 : longest/2+1;
        
        // return the largest distance
        return std::max({longest, count, beginning});
    }
};
```


