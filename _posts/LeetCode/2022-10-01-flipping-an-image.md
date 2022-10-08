---
layout: post
title: "Flipping An Image Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Two Pointers, Matrix ]
similar: [ Two Pointers ]
featured: false
hidden: false
excerpt: LeetCode 832. Given an n x n binary matrix image, flip the image horizontally, then invert it, and return the resulting image.

---

<br />

## Description

LeetCode Problem 832.

Given an n x n binary matrix image, flip the image horizontally, then invert it, and return the resulting image.

To flip an image horizontally means that each row of the image is reversed.
* For example, flipping [1,1,0] horizontally results in [0,1,1].

To invert an image means that each 0 is replaced by 1, and each 1 is replaced by 0.
* For example, inverting [0,1,1] results in [1,0,0].

Example 1:
```
Input: image = [[1,1,0],[1,0,1],[0,0,0]]
Output: [[1,0,0],[0,1,0],[1,1,1]]
Explanation: First reverse each row: [[0,1,1],[1,0,1],[0,0,0]].
Then, invert the image: [[1,0,0],[0,1,0],[1,1,1]]
```

Example 2:
```
Input: image = [[1,1,0,0],[1,0,0,1],[0,1,1,1],[1,0,1,0]]
Output: [[1,1,0,0],[0,1,1,0],[0,0,0,1],[1,0,1,0]]
Explanation: First reverse each row: [[0,0,1,1],[1,0,0,1],[1,1,1,0],[0,1,0,1]].
Then invert the image: [[1,1,0,0],[0,1,1,0],[0,0,0,1],[1,0,1,0]]
```

Constraints:
* n == image.length
* n == image[i].length
* 1 <= n <= 20
* images[i][j] is either 0 or 1.

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<vector<int>> flipAndInvertImage(vector<vector<int>>& image) {
        vector<vector<int>> ans;
        int size = image.size();
        for (int i = 0; i < size; i++) {
            vector<int> item;
            for (int j = size - 1; j >= 0; j--) {
                if (image[i][j] == 0)
                    item.push_back(1);
                else
                    item.push_back(0);
            }
            ans.push_back(item);
        }
        return ans;
    }
};
```


