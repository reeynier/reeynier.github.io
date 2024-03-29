---
layout: post
title: "Can Place Flowers Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Greedy ]
similar: [ Greedy ]
featured: false
hidden: false
excerpt: LeetCode 605. You have a long flowerbed in which some of the plots are planted, and some are not. However, flowers cannot be planted in adjacent plots.

---

<br />

## Description

LeetCode Problem 605.

You have a long flowerbed in which some of the plots are planted, and some are not. However, flowers cannot be planted in adjacent plots.

Given an integer array flowerbed containing 0's and 1's, where 0 means empty and 1 means not empty, and an integer n, return if n new flowers can be planted in the flowerbed without violating the no-adjacent-flowers rule.

Example 1:
```
Input: flowerbed = [1,0,0,0,1], n = 1
Output: true
```

Example 2:
```
Input: flowerbed = [1,0,0,0,1], n = 2
Output: false
```

Constraints:
* 1 <= flowerbed.length <= 2 * 10^4
* flowerbed[i] is 0 or 1.
* There are no two adjacent flowers in flowerbed.
* 0 <= n <= flowerbed.length

<br />

## Sample C++ Code


```c
class Solution {
public:
    bool canPlaceFlowers(vector<int>& flowerbed, int n) {
        flowerbed.insert(flowerbed.begin(), 0);
        flowerbed.push_back(0);
        for (int i = 1; i < flowerbed.size() - 1; ++i) {
            if (flowerbed[i-1] + flowerbed[i] + flowerbed[i+1] == 0) {
                --n;
                ++i;
            }
        }
        return n <= 0;
    }
};
```


