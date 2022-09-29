---
layout: post
title: "Sliding Puzzle Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Breadth-First Search, Matrix ]
similar: [ Breadth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 773. On an 2 x 3 board, there are five tiles labeled from 1 to 5, and an empty square represented by 0. A move consists of choosing 0 and a 4-directionally adjacent number and swapping it.

---

<br />

## Description

LeetCode Problem 773.

On an 2 x 3 board, there are five tiles labeled from 1 to 5, and an empty square represented by 0. A move consists of choosing 0 and a 4-directionally adjacent number and swapping it.

The state of the board is solved if and only if the board is [[1,2,3],[4,5,0]].
Given the puzzle board board, return the least number of moves required so that the state of the board is solved. If it is impossible for the state of the board to be solved, return -1.

Example 1: 
```
Input: board = [[1,2,3],[4,0,5]]
Output: 1
Explanation: Swap the 0 and the 5 in one move.
```

Example 2: 
```
Input: board = [[1,2,3],[5,4,0]]
Output: -1
Explanation: No number of moves will make the board solved.
```

Example 3: 
```
Input: board = [[4,1,2],[5,0,3]]
Output: 5
Explanation: 5 is the smallest number of moves that solves the board.
An example path:
After move 0: [[4,1,2],[5,0,3]]
After move 1: [[4,1,2],[0,5,3]]
After move 2: [[0,1,2],[4,5,3]]
After move 3: [[1,0,2],[4,5,3]]
After move 4: [[1,2,0],[4,5,3]]
After move 5: [[1,2,3],[4,5,0]]
```

Example 4: 
```
Input: board = [[3,2,4],[1,5,0]]
Output: 14
```

Constraints:
* board.length == 2
* board[i].length == 3
* 0 <= board[i][j] <= 5
* Each value board[i][j] is unique.

<br />

## Sample C++ Code


```c
class Solution {
public:
    int slidingPuzzle(vector<vector<int>>& board) {
        int res = 0;
        string end = "123450";
        vector<vector<int>> moves = { {1,3}, {0,2,4}, {1,5}, {0,4}, {1,3,5}, {2,4} };
        
        string begin = "";
        for (int i = 0; i < board.size(); i++) {
            for (int j = 0; j < board[0].size(); j++) {
                begin += to_string(board[i][j]);
            }
        }
        
        unordered_set<string> visited;
        visited.insert(begin);
        queue<pair<string, int>> q;
        q.push({begin, 0});
        while (!q.empty()) {
            auto p = q.front(); q.pop();
            string curr = p.first;
            int dist = p.second;
            int idx = curr.find("0");
            if (curr == end)
                return dist;
            for (auto &i : moves[idx]) {
                string next = curr;
                swap(next[idx], next[i]);
                if (!visited.count(next)) {
                    visited.insert(next);
                    q.push({next, dist + 1});
                }
            }
        }
        
        return -1;
    }
};
```


