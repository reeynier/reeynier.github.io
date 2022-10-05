---
layout: post
title: "Hand Of Straights Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Hash Table, Greedy, Sorting ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 846. Alice has some number of cards and she wants to rearrange the cards into groups so that each group is of size groupSize, and consists of groupSize consecutive cards.

---

<br />

## Description

LeetCode Problem 846.

Alice has some number of cards and she wants to rearrange the cards into groups so that each group is of size groupSize, and consists of groupSize consecutive cards.

Given an integer array hand where hand[i] is the value written on the i^th card and an integer groupSize, return true if she can rearrange the cards, or false otherwise.

Example 1:
```
Input: hand = [1,2,3,6,2,3,4,7,8], groupSize = 3
Output: true
Explanation: Alice's hand can be rearranged as [1,2,3],[2,3,4],[6,7,8]
```

Example 2:
```
Input: hand = [1,2,3,4,5], groupSize = 4
Output: false
Explanation: Alice's hand can not be rearranged into groups of 4.
```

Constraints:
* 1 <= hand.length <= 10^4
* 0 <= hand[i] <= 10^9
* 1 <= groupSize <= hand.length

<br />

## Sample C++ Code


```c
class Solution {
public:
    bool isNStraightHand(vector<int>& hand, int W) {
        if (hand.size() % W != 0)
            return false;
        
        map<int,int> m;
        for (auto &card : hand)
            m[card]++;
        
        while (m.size()!= 0) {
            int cur = m.begin()->first;
            for (int i = 0; i < W; i++) {
                if (m[cur+i] == 0)
                    return false;   
                else if (--m[cur+i] < 1)
                    m.erase(cur + i);
            } 
        }
        
        return true;
    }
};
```


