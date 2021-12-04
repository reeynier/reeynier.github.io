---
layout: post
title: "Word Break Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Hash Table, String, Dynamic Programming, Trie, Memoization ]
similar: [ Trie ]
featured: false
hidden: false
excerpt: LeetCode 139. Given a string s and a dictionary of strings wordDict, return true if s can be segmented into a space-separated sequence of one or more dictionary words.

---

<br />

## Description

LeetCode Problem 139.

Given a string s and a dictionary of strings wordDict, return true if s can be segmented into a space-separated sequence of one or more dictionary words.

Note that the same word in the dictionary may be reused multiple times in the segmentation.

Example 1:
```
Input: s = "leetcode", wordDict = ["leet","code"]
Output: true
Explanation: Return true because "leetcode" can be segmented as "leet code".
```

Example 2:
```
Input: s = "applepenapple", wordDict = ["apple","pen"]
Output: true
Explanation: Return true because "applepenapple" can be segmented as "apple pen apple".
Note that you are allowed to reuse a dictionary word.
```

Example 3:
```
Input: s = "catsandog", wordDict = ["cats","dog","sand","and","cat"]
Output: false
```

Constraints:
* 1 <= s.length <= 300
* 1 <= wordDict.length <= 1000
* 1 <= wordDict[i].length <= 20
* s and wordDict[i] consist of only lowercase English letters.
* All the strings of wordDict are unique.

<br />

## Sample C++ Code


```c
class Solution {
public:
    struct TrieNode {
        TrieNode* arr[26];
        bool is_end;
        TrieNode() {
            for (int i = 0; i < 26; i ++) {
                arr[i] = nullptr;
            }
            is_end = false;
        }
    };
    
    void insert(TrieNode* root, string s) {
        TrieNode* curr = root;
        for (int i = 0; i < s.size(); i ++) {
            int idx = s[i] - 'a';
            if (curr->arr[idx] == nullptr)
                curr->arr[idx] = new TrieNode();
            curr = curr->arr[idx];
        }
        curr->is_end = true;
    }
    
    bool wordBreak(string s, vector<string>& wordDict) {
        TrieNode* root = new TrieNode();
        for (int i = 0; i < wordDict.size(); i ++) {
            insert(root, wordDict[i]);
        }
        
        int l = s.size();
        vector<int> dp(l+1, 0);
        dp[0] = 1;
        
        for (int i = 0; i < l; i ++) {
            if (dp[i] == 0)
                continue;
            TrieNode* curr = root;
            for (int j = i; j < l; j ++) {
                if (curr->arr[s[j]-'a'] == NULL)
                    break;
                curr = curr->arr[s[j]-'a'];
                if (curr->is_end == true)
                    dp[j+1] = 1;
            }
        }
        
        return dp[l];
    }
};
```


