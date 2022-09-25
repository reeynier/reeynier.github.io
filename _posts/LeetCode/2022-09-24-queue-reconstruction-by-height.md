---
layout: post
title: "Queue Reconstruction By Height Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Greedy, Binary Indexed Tree, Segment Tree, Sorting ]
similar: [ Sorting ]
featured: false
hidden: false
excerpt: LeetCode 406. You are given an array of people, people, which are the attributes of some people in a queue (not necessarily in order). Each people[i] = [h_i, k_i] represents the i^th person of height h_i with exactly k_i other people in front who have a height greater than or equal to h_i.

---

<br />

## Description

LeetCode Problem 406.

You are given an array of people, people, which are the attributes of some people in a queue (not necessarily in order). Each people[i] = [h_i, k_i] represents the i^th person of height h_i with exactly k_i other people in front who have a height greater than or equal to h_i.

Reconstruct and return the queue that is represented by the input array people. The returned queue should be formatted as an array queue, where queue[j] = [h_j, k_j] is the attributes of the j^th person in the queue (queue[0] is the person at the front of the queue).

Example 1:
```
Input: people = [[7,0],[4,4],[7,1],[5,0],[6,1],[5,2]]
Output: [[5,0],[7,0],[5,2],[6,1],[4,4],[7,1]]
Explanation:
Person 0 has height 5 with no other people taller or the same height in front.
Person 1 has height 7 with no other people taller or the same height in front.
Person 2 has height 5 with two persons taller or the same height in front, which is person 0 and 1.
Person 3 has height 6 with one person taller or the same height in front, which is person 1.
Person 4 has height 4 with four people taller or the same height in front, which are people 0, 1, 2, and 3.
Person 5 has height 7 with one person taller or the same height in front, which is person 1.
Hence [[5,0],[7,0],[5,2],[6,1],[4,4],[7,1]] is the reconstructed queue.
```

Example 2:
```
Input: people = [[6,0],[5,0],[4,0],[3,2],[2,2],[1,4]]
Output: [[4,0],[5,0],[2,2],[3,2],[1,4],[6,0]]
```

Constraints:
* 1 <= people.length <= 2000
* 0 <= h_i <= 10^6
* 0 <= k_i < people.length
* It is guaranteed that the queue can be reconstructed.

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<vector<int>> reconstructQueue(vector<vector<int>>& people) {
        sort(people.begin(), people.end(), cmp);
        vector<vector<int>> res;
        for (int i = 0; i < people.size(); i++) {
            res.insert(res.begin() + people[i][1], people[i]);
        }
        return res;
    }
    static bool cmp(vector<int>& p1, vector<int>& p2) {
        if (p1[0] != p2[0]) return p1[0] > p2[0];
        else return p1[1] < p2[1];
    }
};
```


