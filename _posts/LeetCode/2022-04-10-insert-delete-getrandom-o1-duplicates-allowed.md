---
layout: post
title: "Insert Delete Getrandom O(1) - Duplicates Allowed Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Hash Table, Math, Design, Randomized ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 381. RandomizedCollection is a data structure that contains a collection of numbers, possibly duplicates (i.e., a multiset). It should support inserting and removing specific elements and also removing a random element.

---

<br />

## Description

LeetCode Problem 381.

RandomizedCollection is a data structure that contains a collection of numbers, possibly duplicates (i.e., a multiset). It should support inserting and removing specific elements and also removing a random element.

Implement the RandomizedCollection class:
* RandomizedCollection() Initializes the empty RandomizedCollection object.
* bool insert(int val) Inserts an item val into the multiset, even if the item is already present. Returns true if the item is not present, false otherwise.
* bool remove(int val) Removes an item val from the multiset if present. Returns true if the item is present, false otherwise. Note that if val has multiple occurrences in the multiset, we only remove one of them.
* int getRandom() Returns a random element from the current multiset of elements. The probability of each element being returned is linearly related to the number of same values the multiset contains.

You must implement the functions of the class such that each function works on average O(1) time complexity.

Note: The test cases are generated such that getRandom will only be called if there is at least one item in the RandomizedCollection.

Example 1:
```
Input
["RandomizedCollection", "insert", "insert", "insert", "getRandom", "remove", "getRandom"]
[[], [1], [1], [2], [], [1], []]
Output
[null, true, false, true, 2, true, 1]
Explanation
RandomizedCollection randomizedCollection = new RandomizedCollection();
randomizedCollection.insert(1);   // return true since the collection does not contain 1.
// Inserts 1 into the collection.
randomizedCollection.insert(1);   // return false since the collection contains 1.
// Inserts another 1 into the collection. Collection now contains [1,1].
randomizedCollection.insert(2);   // return true since the collection does not contain 2.
// Inserts 2 into the collection. Collection now contains [1,1,2].
randomizedCollection.getRandom(); // getRandom should:
// - return 1 with probability 2/3, or
// - return 2 with probability 1/3.
randomizedCollection.remove(1);   // return true since the collection contains 1.
// Removes 1 from the collection. Collection now contains [1,2].
randomizedCollection.getRandom(); // getRandom should return 1 or 2, both equally likely.
```

Constraints:
* -2^31 <= val <= 2^31 - 1
* At most 2 * 10^5 calls in total will be made to insert, remove, and getRandom.
* There will be at least one element in the data structure when getRandom is called.

<br />

## Sample C++ Code


```c
class RandomizedCollection {
public:
    unordered_map<int, vector<int>> um;
    vector<int> v;
    
    /** Initialize your data structure here. */
    RandomizedCollection() {
        
    }
    
    /** Inserts a value to the collection. Returns true if the collection did not already contain the specified element. */
    bool insert(int val) {
        auto mit = um.find(val);
        bool succ = true;
        if (mit == um.end()) {
            vector<int> v_tmp;
            v_tmp.push_back(v.size());
            um[val] = v_tmp;
            v.push_back(val);
            succ = true;
        } else {
            mit->second.push_back(v.size());
            v.push_back(val);
            succ = false;
        }
        return succ;
    }
    
    /** Removes a value from the collection. Returns true if the collection contained the specified element. */
    bool remove(int val) {
        auto mit = um.find(val);
        if (mit == um.end())
            return false;
        int last_val = v.back();
        v.pop_back();
        int idx = mit->second.back();
        v[idx] = last_val;

        int l = um[last_val].size();
        um[last_val][l-1] = idx;
        sort(um[last_val].begin(), um[last_val].end());
        
        if (mit->second.size() == 1)
            um.erase(mit);
        else
            mit->second.pop_back();
        return true;
    }
    
    /** Get a random element from the collection. */
    int getRandom() {
        return v[rand() % v.size()];
    }
};

/**
 * Your RandomizedCollection object will be instantiated and called as such:
 * RandomizedCollection* obj = new RandomizedCollection();
 * bool param_1 = obj->insert(val);
 * bool param_2 = obj->remove(val);
 * int param_3 = obj->getRandom();
 */
```


