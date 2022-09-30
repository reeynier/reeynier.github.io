---
layout: post
title: "Card Flipping Game Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Hash Table ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 822. You are given n cards, with a positive integer printed on the front and back of each card (possibly different). You can flip any number of cards (possibly zero).

---

<br />

## Description

LeetCode Problem 822.

You are given n cards, with a positive integer printed on the front and back of each card (possibly different). You can flip any number of cards (possibly zero).

After choosing the front and the back of each card, you will pick each card, and if the integer printed on the back of this card is not printed on the front of any other card, then this integer is good.

You are given two integer array fronts and backs where fronts[i] and backs[i] are the integers printer on the front and the back of the i^th card respectively.

Return the smallest good and integer after flipping the cards. If there are no good integers, return 0.

Note that a flip swaps the front and back numbers, so the value on the front is now on the back and vice versa.

Example 1:
```
Input: fronts = [1,2,4,4,7], backs = [1,3,4,1,3]
Output: 2
Explanation: If we flip the second card, the fronts are [1,3,4,4,7] and the backs are [1,2,4,1,3].
We choose the second card, which has the number 2 on the back, and it is not on the front of any card, so 2 is good.
```

Example 2:
```
Input: fronts = [1], backs = [1]
Output: 0
```

Constraints:
* n == fronts.length
* n == backs.length
* 1 <= n <= 1000
* 1 <= fronts[i], backs[i] <= 2000

<br />

## Sample C++ Code


```c
class Solution {
public:
    int flipgame(vector<int>& front, vector<int>& back) {
        int n = front.size(), ans = INT_MAX;
        unordered_map<int, int> um;
        for (int i = 0; i < n; i++) {
            if (front[i] == back[i])
                um[front[i]]++;
        }
        for (int i = 0; i < n; i++) {
            if (!um.count(front[i])) {
                ans = min(ans, front[i]);
                um[front[i]]++;
            }
            if (!um.count(back[i])) {
                ans = min(ans, back[i]);
                um[back[i]]++;
            }
        }
        if (ans == INT_MAX)
            return 0;
        return ans;
    }
};
```


