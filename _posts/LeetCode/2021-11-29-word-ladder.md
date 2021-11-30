---
layout: post
title: "Word Ladder Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Hash Table, String, Breadth-First Search ]
similar: [ Breadth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 127. Given two words, beginWord and endWord, and a dictionary wordList, return the number of words in the shortest transformation sequence from beginWord to endWord, or 0 if no such sequence exists.
---

<br />

## Description

LeetCode Problem 127.

A transformation sequence from word beginWord to word endWord using a dictionary wordList is a sequence of words beginWord -> s_1 -> s_2 -> ... -> s_k such that:
* Every adjacent pair of words differs by a single letter.
* Every s_i for 1 <= i <= k is in wordList. Note that beginWord does not need to be in wordList.
* s_k == endWord

Given two words, beginWord and endWord, and a dictionary wordList, return the number of words in the shortest transformation sequence from beginWord to endWord, or 0 if no such sequence exists.

Example 1:
```
Input: beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log","cog"]
Output: 5
Explanation: One shortest transformation sequence is "hit" -> "hot" -> "dot" -> "dog" -> cog", which is 5 words long.
```

Example 2:
```
Input: beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log"]
Output: 0
Explanation: The endWord "cog" is not in wordList, therefore there is no valid transformation sequence.
```

Constraints:
* 1 <= beginWord.length <= 10
* endWord.length == beginWord.length
* 1 <= wordList.length <= 5000
* wordList[i].length == beginWord.length
* beginWord, endWord, and wordList[i] consist of lowercase English letters.
* beginWord != endWord
* All the words in wordList are unique.

<br />

## Sample C++ Code


```c
class Solution {
public:
    int ladderLength(string beginWord, string endWord, vector<string>& wordList) {
        int steps = 0;
        unordered_map<string, int> visited;
        
        for (int i = 0; i < wordList.size(); i ++) {
            visited[wordList[i]] = 0;
        }
        if (visited.find(endWord) == visited.end())
            return steps;
        
        queue<string> bfsQ;
        bfsQ.push(beginWord);
        int l;
        string curr, temp;
        bool found = false;
        while (!bfsQ.empty()) {
            l = bfsQ.size();
            for (int i = 0; i < l; i ++) {
                curr = bfsQ.front();
                bfsQ.pop();
                if (curr == endWord) {
                    found = true;
                    break;
                }
                for (int j = 0; j < curr.size(); j ++) {
                    temp = curr;
                    for (char c = 'a'; c <= 'z'; c ++) {
                        temp[j] = c;
                        if (visited.find(temp) != visited.end()) {
                            if (visited[temp] == 0) {
                                bfsQ.push(temp);
                                visited[temp] = 1;
                            }
                        }
                    }
                }
            }
            steps ++;
            if (found)
                break;
        }
        if (found)
            return steps;
        else
            return 0;
    }
};
```


