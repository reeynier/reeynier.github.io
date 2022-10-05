---
layout: post
title: "Walking Robot Simulation Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Simulation ]
similar: [ Array ]
featured: false
hidden: false
excerpt: LeetCode 874. A robot on an infinite XY-plane starts at point (0, 0) facing north. The robot can receive a sequence of these three possible types of commands

---

<br />

## Description

LeetCode Problem 874.

A robot on an infinite XY-plane starts at point (0, 0) facing north. The robot can receive a sequence of these three possible types of commands:
* -2: Turn left 90 degrees.
* -1: Turn right 90 degrees.
* 1 <= k <= 9: Move forward k units, one unit at a time.

Some of the grid squares are obstacles. The i^th obstacle is at grid point obstacles[i] = (x_i, y_i). If the robot runs into an obstacle, then it will instead stay in its current location and move on to the next command.

Return the maximum Euclidean distance that the robot ever gets from the origin squared (i.e. if the distance is 5, return 25).

Note:
* North means +Y direction.
* East means +X direction.
* South means -Y direction.
* West means -X direction.

Example 1:
```
Input: commands = [4,-1,3], obstacles = []
Output: 25
Explanation: The robot starts at (0, 0):
1. Move north 4 units to (0, 4).
2. Turn right.
3. Move east 3 units to (3, 4).
The furthest point the robot ever gets from the origin is (3, 4), which squared is 3^2 + 4^2 = 25 units away.
```

Example 2:
```
Input: commands = [4,-1,4,-2,4], obstacles = [[2,4]]
Output: 65
Explanation: The robot starts at (0, 0):
1. Move north 4 units to (0, 4).
2. Turn right.
3. Move east 1 unit and get blocked by the obstacle at (2, 4), robot is at (1, 4).
4. Turn left.
5. Move north 4 units to (1, 8).
The furthest point the robot ever gets from the origin is (1, 8), which squared is 1^2 + 8^2 = 65 units away.
```

Example 3:
```
Input: commands = [6,-1,-1,6], obstacles = []
Output: 36
Explanation: The robot starts at (0, 0):
1. Move north 6 units to (0, 6).
2. Turn right.
3. Turn right.
4. Move south 6 units to (0, 0).
The furthest point the robot ever gets from the origin is (0, 6), which squared is 6^2 = 36 units away.
```

Constraints:
* 1 <= commands.length <= 10^4
* commands[i] is either -2, -1, or an integer in the range [1, 9].
* 0 <= obstacles.length <= 10^4
* -3 * 10^4 <= x_i, y_i <= 3 * 10^4
* The answer is guaranteed to be less than 2^31.

<br />

## Sample C++ Code


```c
class Solution {
public:
    int robotSim(vector<int>& commands, vector<vector<int>>& obstacles) {
        unordered_set<string> obs;
        for (int i = 0; i < obstacles.size(); i++) 
            obs.insert(to_string(obstacles[i][0]) + "#" + to_string(obstacles[i][1]));
        int res = 0, dir = 0, x = 0, y = 0;
        vector<vector<int>> ds={ {0, 1}, {1, 0}, {0, -1}, {-1, 0} };
        for (int i = 0; i < commands.size(); i++) {
            if (commands[i] == -2) 
                dir--;
            else if (commands[i] == -1) 
                dir++;
            else {
                for (int j = 0; j < commands[i]; j++) {
                    string pos = to_string(x + ds[dir][0]) + "#" + to_string(y + ds[dir][1]);
                    if (obs.find(pos) != obs.end()) 
                        break;
                    x += ds[dir][0], y += ds[dir][1];
                }
                res = max(res, x * x + y * y);
            }
            if (dir == -1) 
                dir = 3;
            if (dir == 4) 
                dir = 0;
        }
        return res;
    }
};
```


