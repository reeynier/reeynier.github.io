---
layout: post
title: "Champagne Tower Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Dynamic Programming ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 799. We stack glasses in a pyramid, where the first row has 1 glass, the second row has 2 glasses, and so on until the 100^th row. Each glass holds one cupof champagne.

---

<br />

## Description

LeetCode Problem 799.

We stack glasses in a pyramid, where the first row has 1 glass, the second row has 2 glasses, and so on until the 100^th row. Each glass holds one cupof champagne.

Then, some champagne is poured into the first glass at the top. When the topmost glass is full, any excess liquid poured will fall equally to the glass immediately to the left and right of it. When those glasses become full, any excess champagne will fall equally to the left and right of those glasses, and so on. (A glass at the bottom row has its excess champagne fall on the floor.)

For example, after one cup of champagne is poured, the top most glass is full. After two cups of champagne are poured, the two glasses on the second row are half full. After three cups of champagne are poured, those two cups become full - there are 3 full glasses total now. After four cups of champagne are poured, the third row has the middle glass half full, and the two outside glasses are a quarter full.

Now after pouring some non-negative integer cups of champagne, return how full the j^th glass in the i^th row is (both i and j are 0-indexed.)

Example 1:
```
Input: poured = 1, query_row = 1, query_glass = 1
Output: 0.00000
Explanation: We poured 1 cup of champange to the top glass of the tower (which is indexed as (0, 0)). There will be no excess liquid so all the glasses under the top glass will remain empty.
```

Example 2:
```
Input: poured = 2, query_row = 1, query_glass = 1
Output: 0.50000
Explanation: We poured 2 cups of champange to the top glass of the tower (which is indexed as (0, 0)). There is one cup of excess liquid. The glass indexed as (1, 0) and the glass indexed as (1, 1) will share the excess liquid equally, and each will get half cup of champange.
```

Example 3:
```
Input: poured = 100000009, query_row = 33, query_glass = 17
Output: 1.00000
```

Constraints:
* 0 <=poured <= 10^9
* 0 <= query_glass <= query_row< 100

<br />

## Sample C++ Code


```c
class Solution {
public:
    // We use a table to record the result.
    // If the glass >=1, we should split the diff (glass - 1) into next level.
    double champagneTower(int poured, int query_row, int query_glass) {
        double result[101][101] = {0.0};
        result[0][0] = poured;
        for (int i = 0; i < 100; i++) {
            for (int j = 0; j <= i; j++) {
                if (result[i][j] >= 1) {
                    result[i + 1][j] += (result[i][j] - 1) / 2.0;
                    result[i + 1][j + 1] += (result[i][j] - 1) / 2.0;
                    result[i][j] = 1;
                }
            }
        }
        return result[query_row][query_glass];
    }
};
```


