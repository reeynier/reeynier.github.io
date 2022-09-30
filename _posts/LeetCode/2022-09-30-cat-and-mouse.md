---
layout: post
title: "Cat And Mouse Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math, Dynamic Programming, Graph, Topological Sort ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 913. A game on an undirected graph is played by two players, Mouse and Cat, who alternate turns.

---

<br />

## Description

LeetCode Problem 913.

A game on an undirected graph is played by two players, Mouse and Cat, who alternate turns.

The graph is given as follows: graph[a] is a list of all nodes b such that ab is an edge of the graph.

The mouse starts at node 1 and goes first, the cat starts at node 2 and goes second, and there is a hole at node 0.

During each player's turn, they must travel along oneedge of the graph that meets where they are. For example, if the Mouse is at node 1, it must travel to any node in graph[1].

Additionally, it is not allowed for the Cat to travel to the Hole (node 0.)
Then, the game can end in threeways:
* If ever the Cat occupies the same node as the Mouse, the Cat wins.
* If ever the Mouse reaches the Hole, the Mouse wins.
* If ever a position is repeated (i.e., the players are in the same position as a previous turn, andit is the same player's turn to move), the game is a draw.

Given a graph, and assuming both players play optimally, return
* 1if the mouse wins the game,
* 2if the cat wins the game, or
* 0if the game is a draw.

Example 1: 
```
Input: graph = [[2,5],[3],[0,4,5],[1,4,5],[2,3],[0,2,3]]
Output: 0
```

Example 2: 
```
Input: graph = [[1,3],[0],[3],[0,2]]
Output: 1
```

Constraints:
* 3 <= graph.length <= 50
* 1<= graph[i].length < graph.length
* 0 <= graph[i][j] < graph.length
* graph[i][j] != i
* graph[i] is unique.
* The mouse and the cat can always move.

<br />

## Sample C++ Code


```c
class Solution {
public:
    int catMouseGame(vector<vector<int>>& graph) {
        int N = graph.size();
        vector<vector<int>> dp[2];
        vector<vector<int>> outdegree[2];
        queue<vector<int>> q; // q of {turn, mouse position, cat position} for topological sort

        dp[0] = vector<vector<int>>(N, vector<int>(N));
        dp[1] = vector<vector<int>>(N, vector<int>(N));
        outdegree[0] = vector<vector<int>>(N, vector<int>(N));
        outdegree[1] = vector<vector<int>>(N, vector<int>(N));

        // init dp and queue
        for (int j = 0; j < N; ++j) {
            dp[0][0][j] = dp[1][0][j] = 1;
            q.push({0, 0, j});
            q.push({1, 0, j});
        }
        for (int j = 1; j < N; ++j) {
            dp[0][j][j] = dp[1][j][j] = 2;
            q.push({0, j, j});
            q.push({1, j, j});
        }
        // init outdegree
        for (int i = 0; i < N; ++i) {
            for (int j = 1; j < N; ++j) {
                outdegree[0][i][j] = graph[i].size();
                outdegree[1][i][j] = graph[j].size();
            }
        }
        for (auto &v : graph[0]) {
            for (int i = 0; i < N; ++i) {
                outdegree[1][i][v]--;
            }
        }
        // run the topological sort from queue
        while (q.size()) {
            auto turn = q.front()[0];
            auto mouse = q.front()[1];
            auto cat = q.front()[2];
            q.pop();

            if (turn == 0 && mouse == 1 && cat == 2) {
                // the result has been inferenced
                break;
            }

            if (turn == 0) { // mouse's turn
                // v is the prev position of cat
                for (auto &v : graph[cat]) {
                    if (v == 0) 
                        continue;

                    if (dp[1][mouse][v] > 0) 
                        continue;

                    if (dp[turn][mouse][cat] == 2) {
                        // cat wants to move from v to `cat` position, and thus cat wins
                        dp[1][mouse][v] = 2;
                        q.push({1, mouse, v});
                        continue;
                    }

                    outdegree[1][mouse][v]--;
                    if (outdegree[1][mouse][v] == 0) {
                        dp[1][mouse][v] = 1;
                        q.push({1, mouse, v});
                    }
                }
            } else { // cat's turn
                // v is the prev position of mouse
                for (auto &v : graph[mouse]) {
                    if (dp[0][v][cat] > 0) 
                        continue;

                    if (dp[turn][mouse][cat] == 1) {
                        // mouse wants to move from v to `mouse` position and thus mouse wins
                        dp[0][v][cat] = 1;
                        q.push({0, v, cat});
                        continue;
                    }

                    outdegree[0][v][cat]--;
                    if (outdegree[0][v][cat] == 0) {
                        dp[0][v][cat] = 2;
                        q.push({0, v, cat});
                    }
                }
            }
        }

        return dp[0][1][2];
    }
};
```


