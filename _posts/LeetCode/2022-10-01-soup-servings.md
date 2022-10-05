---
layout: post
title: "Soup Servings Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math, Dynamic Programming ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 808. There are two types of soup, type A and type B. Initially, we have n ml of each type of soup. There are four kinds of operations

---

<br />

## Description

LeetCode Problem 808.

There are two types of soup: type A and type B. Initially, we have n ml of each type of soup. There are four kinds of operations:
* Serve 100 ml of soup A and 0 ml of soup B,
* Serve 75 ml of soup A and 25 ml of soup B,
* Serve 50 ml of soup A and 50 ml of soup B, and
* Serve 25 ml of soup A and 75 ml of soup B.

When we serve some soup, we give it to someone, and we no longer have it. Each turn, we will choose from the four operations with an equal probability 0.25. If the remaining volume of soup is not enough to complete the operation, we will serve as much as possible. We stop once we no longer have some quantity of both types of soup.

Note that we do not have an operation where all 100 ml's of soup B are used first.

Return the probability that soup A will be empty first, plus half the probability that A and B become empty at the same time. Answers within 10^-5 of the actual answer will be accepted.

Example 1:
```
Input: n = 50
Output: 0.62500
Explanation: If we choose the first two operations, A will become empty first.
For the third operation, A and B will become empty at the same time.
For the fourth operation, B will become empty first.
So the total probability of A becoming empty first plus half the probability that A and B become empty at the same time, is 0.25 * (1 + 1 + 0.5 + 0) = 0.625.
```

Example 2:
```
Input: n = 100
Output: 0.71875
```

Constraints:
* 0 <= n <= 10^9

<br />

## Sample C++ Code


```c
class Solution {
public:
    double soupServings(int N) {
        const static pair<int,int> moves[4] = { {-4, 0}, {-3, -1}, {-2, -2}, {-1, -3} };
        if (N > 4800)
            return 1.0;
        double dp[256][256] = {0};
        int n = (N + 24) / 25;
        for (int a = 0; a <= n; ++a) {
            for (int b = 0; b <= n; ++b) {
                for (auto &[i,j]: moves) {
                    int x = a + i;
                    int y = b + j;
                    if (x <= 0 and y <= 0)
                        dp[a][b] += 0.5;
                    else if (x <= 0)
                        dp[a][b] += 1.0;
                    else if (y <= 0)
                        continue;
                    else
                        dp[a][b] += dp[x][y];
                }
                dp[a][b] /= 4;
            }
        }
        return dp[n][n];
    }
};
```


