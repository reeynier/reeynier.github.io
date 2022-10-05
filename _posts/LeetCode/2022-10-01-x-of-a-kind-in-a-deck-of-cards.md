---
layout: post
title: "X Of A Kind In A Deck Of Cards Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Hash Table, Math ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 914. In a deck of cards, each card has an integer written on it.

---

<br />

## Description

LeetCode Problem 914.

In a deck of cards, each card has an integer written on it.

Return true if and only if you can choose X >= 2 such that it is possible to split the entire deck into 1 or more groups of cards, where:
* Each group has exactly X cards.
* All the cards in each group have the same integer.

Example 1:
```
Input: deck = [1,2,3,4,4,3,2,1]
Output: true
Explanation: Possible partition [1,1],[2,2],[3,3],[4,4].
```

Example 2:
```
Input: deck = [1,1,1,2,2,2,3,3]
Output: false
Explanation: No possible partition.
```

Example 3:
```
Input: deck = [1]
Output: false
Explanation: No possible partition.
```

Example 4:
```
Input: deck = [1,1]
Output: true
Explanation: Possible partition [1,1].
```

Example 5:
```
Input: deck = [1,1,2,2,2,2]
Output: true
Explanation: Possible partition [1,1],[2,2],[2,2].
```

Constraints:
* 1 <= deck.length <= 10^4
* 0 <= deck[i] < 10^4

<br />

## Sample C++ Code


```c
class Solution {
public:
    int gcd(int x, int y) {
        return x == 0 ? y : gcd(y % x, x);
    }

    bool hasGroupsSizeX(vector<int>& deck) {
        unordered_map<int, int> m;
        for (int i = 0; i < deck.size(); i ++) {
            if (m.find(deck[i]) == m.end())
                m[deck[i]] = 0;
            m[deck[i]] ++;
        }
        int g = -1;
        for (auto x : m) {
            if (g == -1)
                g = x.second;
            else {
                g = gcd(g, x.second);
                if (g < 2)
                    return false;
            }
        }
        return (g >= 2);
    }
};
```


