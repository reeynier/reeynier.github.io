---
layout: post
title: "Perfect Squares Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math, Dynamic Programming, Breadth-First Search ]
similar: [ Breadth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 279. Given an integer n, return the least number of perfect square numbers that sum to n.

---

<br />

## Description

LeetCode Problem 279.

Given an integer n, return the least number of perfect square numbers that sum to n.

A perfect square is an integer that is the square of an integer; in other words, it is the product of some integer with itself. For example, 1, 4, 9, and 16 are perfect squares while 3 and 11 are not.

Example 1:
```
Input: n = 12
Output: 3
Explanation: 12 = 4 + 4 + 4.
```

Example 2:
```
Input: n = 13
Output: 2
Explanation: 13 = 4 + 9.
```

Constraints:
* 1 <= n <= 10^4

<br />

## Sample C++ Code


```c
class Solution {
public:
    int numSquares(int n) {
        vector<int> squares;
        int i = 1;
        while (i*i <= n) {
            squares.push_back(i*i);
            i ++;
        }
        
        queue<int> bfsQ;
        bfsQ.push(n);
        
        int len, curr, threshold = 0;
        int level = 0;
        while (!bfsQ.empty()) {
            len = bfsQ.size();
            for (int i = 0; i < len; i ++) {
                curr = bfsQ.front();
                bfsQ.pop();
                if (curr == 0) 
                    return level;
                threshold = curr / 3;
                for (int j = squares.size() - 1; j >= 0; j --) {
                    if (squares[j] > curr)
                        continue;
                    bfsQ.push(curr - squares[j]);
                    if (squares[j] < threshold)
                        break;
                }
            }
            level ++;
        }
        return level;
    }
};
```


