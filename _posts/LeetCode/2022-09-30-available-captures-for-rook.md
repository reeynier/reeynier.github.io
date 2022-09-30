---
layout: post
title: "Available Captures For Rook Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Matrix, Simulation ]
similar: [ Matrix ]
featured: false
hidden: false
excerpt: LeetCode 999. On an 8 x 8 chessboard, there is exactly one white rook 'R' and some number of white bishops 'B', black pawns 'p', and empty squares '.'.

---

<br />

## Description

LeetCode Problem 999.

On an 8 x 8 chessboard, there is exactly one white rook 'R' and some number of white bishops 'B', black pawns 'p', and empty squares '.'.

When the rook moves, it chooses one of four cardinal directions (north, east, south, or west), then moves in that direction until it chooses to stop, reaches the edge of the board, captures a black pawn, or is blocked by a white bishop. A rook is considered attacking a pawn if the rook can capture the pawn on the rook's turn. The number of available captures for the white rook is the number of pawns that the rook is attacking.

Return the number of available captures for the white rook.

Example 1: 
```
Input: board = 
[[".",".",".",".",".",".",".","."],
[".",".",".","p",".",".",".","."],
[".",".",".","R",".",".",".","p"],
[".",".",".",".",".",".",".","."],
[".",".",".",".",".",".",".","."],
[".",".",".","p",".",".",".","."],
[".",".",".",".",".",".",".","."],
[".",".",".",".",".",".",".","."]]
Output: 3
Explanation: In this example, the rook is attacking all the pawns.
```

Example 2: 
```
Input: board = 
[[".",".",".",".",".",".",".","."],
[".","p","p","p","p","p",".","."],
[".","p","p","B","p","p",".","."],
[".","p","B","R","B","p",".","."],
[".","p","p","B","p","p",".","."],
[".","p","p","p","p","p",".","."],
[".",".",".",".",".",".",".","."],
[".",".",".",".",".",".",".","."]]
Output: 0
Explanation: The bishops are blocking the rook from attacking any of the pawns.
```

Example 3: 
```
Input: board = 
[[".",".",".",".",".",".",".","."],
[".",".",".","p",".",".",".","."],
[".",".",".","p",".",".",".","."],
["p","p",".","R",".","p","B","."],
[".",".",".",".",".",".",".","."],
[".",".",".","B",".",".",".","."],
[".",".",".","p",".",".",".","."],
[".",".",".",".",".",".",".","."]]
Output: 3
Explanation: The rook is attacking the pawns at positions b5, d6, and f5.
```

Constraints:
* board.length == 8
* board[i].length == 8
* board[i][j] is either 'R', '.', 'B', or 'p'
* There is exactly one cell with board[i][j] == 'R'

<br />

## Sample C++ Code


```c
class Solution {
public:
    int numRookCaptures(vector<vector<char>>& board) {
        int cap = 0, row, col;
        //Find the position of the rook
        for (int i = 0; i < 8; i++) {
            for (int j = 0; j < 8; j++) {
                if (board[i][j] == 'R') {
                    row = i;
                    col = j;
                }
            }
        }
		
        //Move in upward direction to check for any possible captures
        int i = row, j = col;
        while (i >= 0 && board[i][j] != 'B') {
            if (board[i][j] == 'p') {
                cap++;
                break;
            }            
            i--;
        }
		
        //Move in downward direction to check for any possible captures
        i = row, j = col;
        while (i <= 7 && board[i][j] != 'B') {
            if (board[i][j] == 'p') {
                cap++;
                break;
            }            
            i++;
        }
		
        //Move in leftward direction to check for any possible captures
        i = row, j = col;
        while (j >= 0 && board[i][j] != 'B') {
            if (board[i][j] == 'p') {
                cap++;
                break;
            }            
            j--;
        }
		
        //Move in rightward direction to check for any possible captures
        i = row, j = col;
        while (j <= 7 && board[i][j] != 'B') {
            if (board[i][j] == 'p') {
                cap++;
                break;
            }
            j++;
        }
        
        return cap;
    }
};
```


