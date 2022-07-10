---
layout: post
title: "Create Maximum Number Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Stack, Greedy, Monotonic Stack ]
similar: [ Greedy ]
featured: false
hidden: false
excerpt: LeetCode 321. You are given two integer arrays nums1 and nums2 of lengths m and n respectively. nums1 and nums2 represent the digits of two numbers. You are also given an integer k.

---

<br />

## Description

LeetCode Problem 321.

You are given two integer arrays nums1 and nums2 of lengths m and n respectively. nums1 and nums2 represent the digits of two numbers. You are also given an integer k.

Create the maximum number of length k <= m + n from digits of the two numbers. The relative order of the digits from the same array must be preserved.

Return an array of the k digits representing the answer.

Example 1:
```
Input: nums1 = [3,4,6,5], nums2 = [9,1,2,5,8,3], k = 5
Output: [9,8,6,5,3]
```

Example 2:
```
Input: nums1 = [6,7], nums2 = [6,0,4], k = 5
Output: [6,7,6,0,4]
```

Example 3:
```
Input: nums1 = [3,9], nums2 = [8,9], k = 3
Output: [9,8,9]
```

Constraints:
* m == nums1.length
* n == nums2.length
* 1 <= m, n <= 500
* 0 <= nums1[i], nums2[i] <= 9
* 1 <= k <= m + n

<br />

## Sample C++ Code

Basic Idea of this problem is that we have two arrays, so we find the largest 'i' digit number from nums1 and largest 'k-i' digit number from nums2. After having these two, we merge them using merge sort algorithm. We use merge sort because it can be proved that largest number will always be sorted in descending order. The only thing to keep in mind while merging is the case where array elements are equal. In that case, we have to loop untill we find a greater element in one of the two arrays and then act accordingly.

So after finding a i digit number from nums1 and k-i digit number from nums2, we merge them to form the maximum k digit number from these two arrays.


```c
class Solution {
public:
    vector<int> maxNumber(vector<int>& nums1, vector<int>& nums2, int k) {
        vector <int>res;

        for(int i = 0; i<=k; i++){
            vector <int> a = fun(nums1, i);
            vector <int> b = fun(nums2, k-i);

            vector <int> m;
            merge(a, b, m);

            if(m.size()==k) res = max(res,m);
        }
        return res;
    }
protected:
    // This function finds the k digit maximum number possible
    vector <int> fun(vector <int>&nums, int k){
        if(k>nums.size()) return {};
        vector <int> res;
        stack <int> st;
        int rem = k, n = nums.size();
        for(int i = 0; i<n; i++){
            if(st.empty()) st.push(nums[i]), rem--;
            else{
                int avail = n-i;
                while(!st.empty() and st.top()<nums[i] and rem<k and avail>rem) st.pop(), rem++;
                st.push(nums[i]), rem--;
            }
        }
        while(st.size()>k) st.pop();
        while(!st.empty()) res.push_back(st.top()), st.pop();
        reverse(res.begin(), res.end());
        return res;
    }
    void merge(vector <int>&a, vector <int>&b, vector <int>&res){
        int i = 0, j = 0, k = 0;
        // This is the only case which we need to take care of. 
        // Here, we loop until we find a number greater than another 
        // number in other array. When we do that, we push the element 
        // in result array accordingly. 
        while(i<a.size() and j<b.size()){
            if(a[i]==b[j]){
                int ti = i, tj = j;
                while(ti<a.size() and tj<b.size() and a[ti]==b[tj]) ti++, tj++;

                if(tj==b.size()) res.push_back(a[i]), i++;
                else
                if(ti<a.size() and a[ti]>b[tj]) res.push_back(a[i]), i++;
                else res.push_back(b[j]), j++;
            }
            else
            if(a[i]>b[j]) res.push_back(a[i]), i++;
            else res.push_back(b[j]), j++;
        }
        while(i<a.size()) res.push_back(a[i]), i++;
        while(j<b.size()) res.push_back(b[j]), j++;
    }
};
```


