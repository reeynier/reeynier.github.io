---
layout: post
title: "Couples Holding Hands Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Greedy, Depth-First Search, Breadth-First Search, Union Find, Graph ]
similar: [ Depth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 765. There are n couples sitting in 2n seats arranged in a row and want to hold hands.

---

<br />

## Description

LeetCode Problem 765.

There are n couples sitting in 2n seats arranged in a row and want to hold hands.

The people and seats are represented by an integer array row where row[i] is the ID of the person sitting in the i^th seat. The couples are numbered in order, the first couple being (0, 1), the second couple being (2, 3), and so on with the last couple being (2n - 2, 2n - 1).

Return the minimum number of swaps so that every couple is sitting side by side. A swap consists of choosing any two people, then they stand up and switch seats.

Example 1:
```
Input: row = [0,2,1,3]
Output: 1
Explanation: We only need to swap the second (row[1]) and third (row[2]) person.
```

Example 2:
```
Input: row = [3,2,0,1]
Output: 0
Explanation: All couples are already seated side by side.
```

Constraints:
* 2n == row.length
* 2 <= n <= 30
* n is even.
* 0 <= row[i] < 2n
* All the elements of row are unique.

<br />

## Sample C++ Code using Union Find


```c
class UF {
public:
    UF (int n) : parent(n) {}
    
    void setParent(int x, int p) {
        parent[x] = p;
    }
    
    int find(int x) {
        if (x != parent[x])
            parent[x] = find(parent[x]);
        return parent[x];
    }
    
    bool union_find(int x, int y) {
        int px = find(x);
        int py = find(y);
        if (px == py)
            return false;
        parent[px] = py;
        return true;
    }

private:
    vector<int> parent;
};

class Solution {
public:
    int minSwapsCouples(vector<int>& row) {
        if (row.empty()) return 0;
        UF uf(row.size());
        for (int i = 0; i < row.size(); i += 2) {
            uf.setParent(row[i], row[i]);
            uf.setParent(row[i+1], row[i]);
        }
        int counter = 0;
        for (int i = 0; i < row.size(); i += 2) {
            if (uf.union_find(i, i + 1))
                counter++;
        }
        return counter;
    }
};
```


