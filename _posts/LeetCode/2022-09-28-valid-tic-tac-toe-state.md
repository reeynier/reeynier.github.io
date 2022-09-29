---
layout: post
title: "Valid Tic-Tac-Toe State Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, String ]
similar: [ String ]
featured: false
hidden: false
excerpt: LeetCode 794. Given a Tic-Tac-Toe board as a string array board, return true if and only if it is possible to reach this board position during the course of a valid tic-tac-toe game.

---

<br />

## Description

LeetCode Problem 794.

Given a Tic-Tac-Toe board as a string array board, return true if and only if it is possible to reach this board position during the course of a valid tic-tac-toe game.

The board is a 3 x 3 array that consists of characters ' ', 'X', and 'O'. The ' ' character represents an empty square.

Here are the rules of Tic-Tac-Toe:
* Players take turns placing characters into empty squares ' '.
* The first player always places 'X' characters, while the second player always places 'O' characters.
* 'X' and 'O' characters are always placed into empty squares, never filled ones.
* The game ends when there are three of the same (non-empty) character filling any row, column, or diagonal.
* The game also ends if all squares are non-empty.
* No more moves can be played if the game is over.

Example 1: 
```
Input: board = ["O  ","   ","   "]
Output: false
Explanation: The first player always plays "X".
```

Example 2: 
```
Input: board = ["XOX"," X ","   "]
Output: false
Explanation: Players take turns making moves.
```

Example 3: 
```
Input: board = ["XXX","   ","OOO"]
Output: false
```

Example 4: 
```
Input: board = ["XOX","O O","XOX"]
Output: true
```

Constraints:
* board.length == 3
* board[i].length == 3
* board[i][j] is either 'X', 'O', or ' '.

<br />

## Sample C++ Code


```c
class Solution {
public:
    bool iswin(vector<string> &board, char c) {
        return ((board[0][0] == c && board[0][1] == c && board[0][2] == c) ||
          (board[1][0] == c && board[1][1] == c && board[1][2] == c) ||
          (board[2][0] == c && board[2][1] == c && board[2][2] == c) ||
          (board[0][0] == c && board[1][0] == c && board[2][0] == c) ||
          (board[0][1] == c && board[1][1] == c && board[2][1] == c) ||
          (board[0][2] == c && board[1][2] == c && board[2][2] == c) ||
          (board[0][0] == c && board[1][1] == c && board[2][2] == c) ||
          (board[0][2] == c && board[1][1] == c && board[2][0] == c));
    }
    
    bool validTicTacToe(vector<string>& board) {
        int xcnt = 0, ocnt = 0;
        for (string s: board) {
            for (char c: s) {
                if (c == 'X') 
                    xcnt ++;
                else if (c == 'O') 
                    ocnt ++;
            }
        }
        if (xcnt != ocnt && xcnt != ocnt + 1) 
            // X can have equal or only 1 more move than O
            return false;          
        if (iswin(board, 'X') && xcnt != ocnt + 1) 
            // X will win by having one additional move
            return false;     
        if (iswin(board, 'O') && xcnt != ocnt) 
            // since X played first, O can win only when both have made same number of moves
            return false;         
        return true;
    }
};
```


