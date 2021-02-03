---
layout: post
title:  "Insert Delete GetRandom O(1) Problem"
categories: [ Data Structure ]
tags: [ Hash Table, Leetcode ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 380. Implement a RandomizedSet class.
---

<br />

## Description

LeetCode Problem 380. 

Implement the RandomizedSet class:

* bool insert(int val): Inserts an item val into the set if not present. Returns true if the item was not present, false otherwise.
* bool remove(int val): Removes an item val from the set if present. Returns true if the item was present, false otherwise.
* int getRandom(): Returns a random element from the current set of elements (it's guaranteed that at least one element exists when this method is called). Each element must have the same probability of being returned.

Follow up: Could you implement the functions of the class with each function works in average O(1) time?

Example 1:

```
Input
["RandomizedSet", "insert", "remove", "insert", "getRandom", "remove", "insert", "getRandom"]
[[], [1], [2], [2], [], [1], [2], []]
Output
[null, true, false, true, 2, true, false, 2]

Explanation
RandomizedSet randomizedSet = new RandomizedSet();
randomizedSet.insert(1); // Inserts 1 to the set. Returns true as 1 was inserted successfully.
randomizedSet.remove(2); // Returns false as 2 does not exist in the set.
randomizedSet.insert(2); // Inserts 2 to the set, returns true. Set now contains [1,2].
randomizedSet.getRandom(); // getRandom() should return either 1 or 2 randomly.
randomizedSet.remove(1); // Removes 1 from the set, returns true. Set now contains [2].
randomizedSet.insert(2); // 2 was already in the set, so return false.
randomizedSet.getRandom(); // Since 2 is the only number in the set, getRandom() will always return 2.
```

<br />

## Sample C++ Code


This is a C++ solution using a `hash table`.

```c
class RandomizedSet {
private:
    unordered_map<int, int> um;
    vector<int> v;
public:
    /** Initialize your data structure here. */
    RandomizedSet() {
        
    }
    
    /** Inserts a value to the set. Returns true if the set did not already contain the specified element. */
    bool insert(int val) {
        if (um.find(val) != um.end())
            return false;
        um[val] = v.size();
        v.push_back(val);
        return true;
    }
    
    /** Removes a value from the set. Returns true if the set contained the specified element. */
    bool remove(int val) {
        unordered_map<int, int>::iterator mit = um.find(val);
        if (mit == um.end())
            return false;
        int temp = v.back();
        v.pop_back();
        v[mit->second] = temp;
        um[temp] = mit->second;
        um.erase(mit);
        return true;
    }
    
    /** Get a random element from the set. */
    int getRandom() {
        return v[rand() % v.size()];
    }
};

/**
 * Your RandomizedSet object will be instantiated and called as such:
 * RandomizedSet* obj = new RandomizedSet();
 * bool param_1 = obj->insert(val);
 * bool param_2 = obj->remove(val);
 * int param_3 = obj->getRandom();
 */
```
