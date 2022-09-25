---
layout: post
title: "Remove Boxes Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Dynamic Programming, Memoization ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 546. You are given several boxes with different colors represented by different positive numbers.

---

<br />

## Description

LeetCode Problem 546.

You are given several boxes with different colors represented by different positive numbers.

You may experience several rounds to remove boxes until there is no box left. Each time you can choose some continuous boxes with the same color (i.e., composed of k boxes, k >= 1), remove them and get k * k points.

Return the maximum points you can get.

Example 1:
```
Input: boxes = [1,3,2,2,2,3,4,3,1]
Output: 23
Explanation:
[1, 3, 2, 2, 2, 3, 4, 3, 1] 
----> [1, 3, 3, 4, 3, 1] (3*3=9 points) 
----> [1, 3, 3, 3, 1] (1*1=1 points) 
----> [1, 1] (3*3=9 points) 
----> [] (2*2=4 points)
```

Example 2:
```
Input: boxes = [1,1,1]
Output: 9
```

Example 3:
```
Input: boxes = [1]
Output: 1
```

Constraints:
* 1 <= boxes.length <= 100
* 1 <= boxes[i]<= 100

<br />

## Sample C++ Code


```c
class Solution {
public:
	// initialized to 0, mem[left][right][k] means value from boxes[left]~boxes[right] followed by 
    // k same color boxes. Follow does not mean strictly consecutive boxes, 
    // for example, [1, 3, 2, 3, 4], 3 can be 
    // followed by the other 3 because we can remove 2 first
    int mem[100][100][100]; 
    
    int removeBoxes(vector<int>& boxes) {
        return DFS(boxes,0,boxes.size()-1,0);
    }
    
    int DFS(vector<int>& boxes, int l,int r,int k){
        if (l>r) return 0; 
        if (mem[l][r][k]) 
        	// if we have calculated this DFS result, return it
        	return mem[l][r][k]; 
        
        // box[l][r] result is box[l][r-1]+(k+1)^2
        mem[l][r][k] = DFS(boxes,l,r-1,0) + (k+1)*(k+1); 

        for (int i=l; i<r; i++) 
        	// go through each box from left
        	// check for same color box as boxes[r]
            if (boxes[i]==boxes[r]) 
            	// if we found same color box,
                // then we have a chance to get a higher value by group 
                // boxes[l]~boxes[i] and boxes[r] together, plus the 
                // value from boxes[i+1]~boxes[r-1]
                mem[l][r][k] = max(mem[l][r][k], DFS(boxes,l,i,k+1) + DFS(boxes,i+1,r-1,0)); 
        return mem[l][r][k];
    }
};
```


