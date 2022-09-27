---
layout: post
title: "Kth Largest Element In A Stream Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Tree, Design, Binary Search Tree, Heap, Binary Tree, Data Stream ]
similar: [ Design ]
featured: false
hidden: false
excerpt: LeetCode 703. Design a class to find the k^th largest element in a stream. Note that it is the k^th largest element in the sorted order, not the k^th distinct element.

---

<br />

## Description

LeetCode Problem 703.

Design a class to find the k^th largest element in a stream. Note that it is the k^th largest element in the sorted order, not the k^th distinct element.

Implement KthLargest class:
* KthLargest(int k, int[] nums) Initializes the object with the integer k and the stream of integers nums.
* int add(int val) Appends the integer val to the stream and returns the element representing the k^th largest element in the stream.

Example 1:
```
Input
["KthLargest", "add", "add", "add", "add", "add"]
[[3, [4, 5, 8, 2]], [3], [5], [10], [9], [4]]
Output
[null, 4, 5, 5, 8, 8]
Explanation
KthLargest kthLargest = new KthLargest(3, [4, 5, 8, 2]);
kthLargest.add(3);   // return 4
kthLargest.add(5);   // return 5
kthLargest.add(10);  // return 5
kthLargest.add(9);   // return 8
kthLargest.add(4);   // return 8
```

Constraints:
* 1 <= k <= 10^4
* 0 <= nums.length <= 10^4
* -10^4 <= nums[i] <= 10^4
* -10^4 <= val <= 10^4
* At most 10^4 calls will be made to add.
* It is guaranteed that there will be at least k elements in the array when you search for the k^th element.

<br />

## Sample C++ Code


```c
class KthLargest {
public:
    priority_queue<int,vector<int>,greater<int>> pq;
    int K;
    
    KthLargest(int k, vector<int>& nums) {
        K = k;
        for (int i = 0; i < nums.size(); i ++)
            add(nums[i]);
    }
    
    int add(int val) {
        pq.push(val);
        if (pq.size() > K)
            pq.pop();
        return pq.top();
    }
};

/**
 * Your KthLargest object will be instantiated and called as such:
 * KthLargest* obj = new KthLargest(k, nums);
 * int param_1 = obj->add(val);
 */
```


