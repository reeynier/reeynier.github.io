---
layout: post
title: "Construct Quad Tree Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Divide and Conquer, Tree, Matrix ]
similar: [ Tree ]
featured: false
hidden: false
excerpt: LeetCode 427. Given a n * n matrix grid of 0's and 1's only. We want to represent the grid with a Quad-Tree.

---

<br />

## Description

LeetCode Problem 427.

Given a n * n matrix grid of 0's and 1's only. We want to represent the grid with a Quad-Tree.
Return the root of the Quad-Tree representing the grid.

Notice that you can assign the value of a node to True or False when isLeaf is False, and both are accepted in the answer.

A Quad-Tree is a tree data structure in which each internal node has exactly four children. Besides, each node has two attributes:
* val: True if the node represents a grid of 1's or False if the node represents a grid of 0's.
* isLeaf: True if the node is leaf node on the tree or False if the node has the four children.

```
class Node {
public boolean val;
public boolean isLeaf;
public Node topLeft;
public Node topRight;
public Node bottomLeft;
public Node bottomRight;
}
```

We can construct a Quad-Tree from a two-dimensional area using the following steps:
* If the current grid has the same value (i.e all 1's or all 0's)set isLeafTrue and set val to the value of the grid and set the four children to Null and stop.
* If the current grid has different values, set isLeaf to False andset val to any value and divide the current grid into four sub-grids as shown in the photo.
* Recurse for each of the children with the proper sub-grid.

Quad-Treeformat:

The output represents the serialized format of a Quad-Tree using level order traversal, where null signifies a path terminator where no node exists below.

It is very similar to the serialization of the binary tree. The only difference is that the node is represented as a list [isLeaf, val].

If the value of isLeaf or val is True we represent it as 1 in the list[isLeaf, val] and if the value of isLeaf or val is False we represent it as 0.

Example 1:
```
Input: grid = [[0,1],[1,0]]
Output: [[0,1],[1,0],[1,1],[1,1],[1,0]]
Explanation: The explanation of this example is shown below:
Notice that 0 represnts False and 1 represents True in the photo representing the Quad-Tree.
<img alt="" src="https://assets.leetcode.com/uploads/2020/02/12/e1tree.png" style="width: 777px; height: 186px;" />
```

Example 2:
```
Input: grid = [[1,1,1,1,0,0,0,0],[1,1,1,1,0,0,0,0],[1,1,1,1,1,1,1,1],[1,1,1,1,1,1,1,1],[1,1,1,1,0,0,0,0],[1,1,1,1,0,0,0,0],[1,1,1,1,0,0,0,0],[1,1,1,1,0,0,0,0]]
Output: [[0,1],[1,1],[0,1],[1,1],[1,0],null,null,null,null,[1,0],[1,0],[1,1],[1,1]]
Explanation: All values in the grid are not the same. We divide the grid into four sub-grids.
The topLeft, bottomLeft and bottomRight each has the same value.
The topRight have different values so we divide it into 4 sub-grids where each has the same value.
Explanation is shown in the photo below:
<img alt="" src="https://assets.leetcode.com/uploads/2020/02/12/e2tree.png" style="width: 777px; height: 328px;" />
```

Example 3:
```
Input: grid = [[1,1],[1,1]]
Output: [[1,1]]
```

Example 4:
```
Input: grid = [[0]]
Output: [[1,0]]
```

Example 5:
```
Input: grid = [[1,1,0,0],[1,1,0,0],[0,0,1,1],[0,0,1,1]]
Output: [[0,1],[1,1],[1,0],[1,0],[1,1]]
```

Constraints:
* n == grid.length == grid[i].length
* n == 2^x where 0 <= x <= 6

<br />

## Sample C++ Code


```c
/*
// Definition for a QuadTree node.
class Node {
public:
    bool val;
    bool isLeaf;
    Node* topLeft;
    Node* topRight;
    Node* bottomLeft;
    Node* bottomRight;
    
    Node() {
        val = false;
        isLeaf = false;
        topLeft = NULL;
        topRight = NULL;
        bottomLeft = NULL;
        bottomRight = NULL;
    }
    
    Node(bool _val, bool _isLeaf) {
        val = _val;
        isLeaf = _isLeaf;
        topLeft = NULL;
        topRight = NULL;
        bottomLeft = NULL;
        bottomRight = NULL;
    }
    
    Node(bool _val, bool _isLeaf, Node* _topLeft, Node* _topRight, Node* _bottomLeft, Node* _bottomRight) {
        val = _val;
        isLeaf = _isLeaf;
        topLeft = _topLeft;
        topRight = _topRight;
        bottomLeft = _bottomLeft;
        bottomRight = _bottomRight;
    }
};
*/

class Solution {
private:
    Node *constructHelper(vector<vector<int>> &grid, int len, int x, int y) {
        int flag = grid[x][y];
        for (int i = x; i < x + len; i++)
            for (int j = y; j < y + len; j++)
                //if not a leaf, go deeper
                if (flag != grid[i][j]) {
                    Node *tl = constructHelper(grid, len / 2, x, y);
                    Node *tr = constructHelper(grid, len / 2, x, y + len / 2);
                    Node *bl = constructHelper(grid, len / 2, x + len / 2, y);
                    Node *br = constructHelper(grid, len / 2, x + len / 2, y + len / 2);
                    return new Node(true, false, tl, tr, bl, br);
                }
        return new Node(grid[x][y] == 1, true, nullptr, nullptr, nullptr, nullptr);
    }

public:
    Node *construct(vector<vector<int>> &grid) {
        int n = grid.size();
        return (n == 0) ? nullptr : constructHelper(grid, n, 0, 0);
    }
};
```


