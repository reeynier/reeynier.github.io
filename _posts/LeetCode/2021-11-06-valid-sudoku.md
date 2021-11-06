---
layout: post
title:  "Search in Rotated Sorted Array Problem"
categories: [ Data Structure ]
tags: [ Array, Hash Table, Leetcode ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 36. Determine if a 9 x 9 Sudoku board is valid.
---

<br />

## Description

LeetCode Problem 36. 

Determine if a 9 x 9 Sudoku board is valid. Only the filled cells need to be validated according to the following rules:

* Each row must contain the digits 1-9 without repetition.
* Each column must contain the digits 1-9 without repetition.
* Each of the nine 3 x 3 sub-boxes of the grid must contain the digits 1-9 without repetition.

Note:

* A Sudoku board (partially filled) could be valid but is not necessarily solvable.
* Only the filled cells need to be validated according to the mentioned rules.
 

Example 1:
```
Input: board = 
[["5","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]
Output: true
```

Example 2:
```
Input: board = 
[["8","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]
Output: false
Explanation: Same as Example 1, except with the 5 in the top left corner being modified to 8. Since there are two 8's in the top left 3x3 sub-box, it is invalid.
```

Constraints:

* board.length == 9
* board[i].length == 9
* board[i][j] is a digit 1-9 or '.'.


<br />

## Sample C++ Code


```c
class Solution {
public:
    bool isValidSudoku(vector<vector<char>>& board) {
        vector<int> v_h(9, 0);
        vector<int> v_v(9, 0);
        vector<int> v_c(9, 0);
        vector<vector<int>> l = { {1,1}, {1,4}, {1,7}, {4,1}, {4,4}, {4,7}, {7,1}, {7,4}, {7,7} };
        vector<vector<int>> p = { {0,0}, {-1,-1}, {-1,0}, {-1,1}, {0,-1}, {0,1}, {1,-1}, {1,0}, {1,1} };
        for (int i = 0; i < 9; i ++) {
            fill(v_h.begin(), v_h.end(), 0);
            fill(v_v.begin(), v_v.end(), 0);
            fill(v_c.begin(), v_c.end(), 0);
            for (int j = 0; j < 9; j ++) {
                char c = board[i][j];
                if (c != '.') {
                    v_h[c-'0'-1] ++;
                    if (v_h[c-'0'-1] > 1)
                        return false;
                }
                c = board[j][i];
                if (c != '.') {
                    v_v[c-'0'-1] ++;
                    if (v_v[c-'0'-1] > 1)
                        return false;
                }
                c = board[l[i][0]+p[j][0]][l[i][1]+p[j][1]];
                if (c != '.') {
                    v_c[c-'0'-1] ++;
                    if (v_c[c-'0'-1] > 1)
                        return false;
                }
            }
        }
        return true;
    }
};
```
