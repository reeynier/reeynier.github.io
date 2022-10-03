---
layout: post
title: "Magic Squares In Grid Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Math, Matrix ]
similar: [ Math ]
featured: false
hidden: false
excerpt: LeetCode 840. A 3 x 3 magic square is a 3 x 3 grid filled with distinct numbers from 1 to 9 such that each row, column, and both diagonals all have the same sum.

---

<br />

## Description

LeetCode Problem 840.

A 3 x 3 magic square is a 3 x 3 grid filled with distinct numbers from 1 to 9 such that each row, column, and both diagonals all have the same sum.

Given a row x colgridof integers, how many 3 x 3 "magic square" subgrids are there? (Each subgrid is contiguous).

Example 1: 
```
Input: grid = [[4,3,8,4],[9,5,1,9],[2,7,6,2]]
Output: 1
Explanation: 
The following subgrid is a 3 x 3 magic square:
<img alt="" src="https://assets.leetcode.com/uploads/2020/09/11/magic_valid.jpg" style="width: 242px; height: 242px;" />
while this one is not:
<img alt="" src="https://assets.leetcode.com/uploads/2020/09/11/magic_invalid.jpg" style="width: 242px; height: 242px;" />
In total, there is only one magic square inside the given grid.
```

Example 2:
```
Input: grid = [[8]]
Output: 0
```

Example 3:
```
Input: grid = [[4,4],[3,3]]
Output: 0
```

Example 4:
```
Input: grid = [[4,7,8],[9,5,1],[2,3,6]]
Output: 0
```

Constraints:
* row == grid.length
* col == grid[i].length
* 1 <= row, col <= 10
* 0 <= grid[i][j] <= 15

<br />

## Sample C++ Code


```c
class Solution {
public:
    int numMagicSquaresInside(vector<vector<int>>& grid) {
        int result = 0;
        for (int i = 0; i < grid.size(); i++) {
            for (int j = 0; j < grid[i].size() ; j++) {
                if (isMagicSquare(grid, i, j)) {
                    result++;
                }
            }
        }
        return result;
    }
    
    bool isMagicSquare(vector<vector<int>>& grid, int i, int j) {
        if (i + 2 < grid.size() && j+2 < grid[i].size()) {
            int col1 = grid[i][j] + grid[i+1][j] + grid[i+2][j];
            int col2 = grid[i][j+1] + grid[i+1][j+1] + grid[i+2][j+1];
            int col3 = grid[i][j+2] + grid[i+1][j+2] + grid[i+2][j+2];
            int row1 = grid[i][j] + grid[i][j+1] + grid[i][j+2];
            int row2 = grid[i+1][j] + grid[i+1][j+1] + grid[i+1][j+2];
            int row3 = grid[i+2][j] + grid[i+2][j+1] + grid[i+2][j+2];
            int diag1 = grid[i][j] + grid[i+1][j+1] + grid[i+2][j+2];
            int diag2 = grid[i+2][j] + grid[i+1][j+1] + grid[i][j+2];
            if ((col1 == col2) &&
                (col1 == col3) &&
                (col1 == row1) && 
                (col1 == row2) &&
                (col1 == row3) &&
                (col1 == diag1) &&
                (col1 == diag2)) {
                set<int> s({1, 2, 3, 4, 5, 6, 7, 8, 9});
                for (int r = 0 ; r < 3 ; r++) {
                    for (int c = 0; c < 3 ; c++) {
                        s.erase(grid[i + r][j + c]);
                    }
                }
                return s.empty();
            }
        }
        return false;
    }
};
```


