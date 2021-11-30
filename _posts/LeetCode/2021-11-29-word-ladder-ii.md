---
layout: post
title: "Word Ladder II Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Hash Table, String, Backtracking, Breadth-First Search ]
similar: [ Breadth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 126. Given two words, beginWord and endWord, and a dictionary wordList, return all the shortest transformation sequences from beginWord to endWord, or an empty list if no such sequence exists.
---

<br />

## Description

LeetCode Problem 126.

A transformation sequence from word beginWord to word endWord using a dictionary wordList is a sequence of words beginWord -> s_1 -> s_2 -> ... -> s_k such that:
* Every adjacent pair of words differs by a single letter.
* Every s_i for 1 <= i <= k is in wordList. Note that beginWord does not need to be in wordList.
* s_k == endWord

Given two words, beginWord and endWord, and a dictionary wordList, return all the shortest transformation sequences from beginWord to endWord, or an empty list if no such sequence exists. Each sequence should be returned as a list of the words [beginWord, s_1, s_2, ..., s_k].

Example 1:
```
Input: beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log","cog"]
Output: [["hit","hot","dot","dog","cog"],["hit","hot","lot","log","cog"]]
Explanation:There are 2 shortest transformation sequences:
"hit" -> "hot" -> "dot" -> "dog" -> "cog"
"hit" -> "hot" -> "lot" -> "log" -> "cog"
```

Example 2:
```
Input: beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log"]
Output: []
Explanation: The endWord "cog" is not in wordList, therefore there is no valid transformation sequence.
```

Constraints:
* 1 <= beginWord.length <= 5
* endWord.length == beginWord.length
* 1 <= wordList.length <= 1000
* wordList[i].length == beginWord.length
* beginWord, endWord, and wordList[i] consist of lowercase English letters.
* beginWord != endWord
* All the words in wordList are unique.

<br />

## Sample C++ Code


```c
vector<vector<string>> findLadders(string beginWord, string endWord, unordered_set<string> &wordList) { 
    // The idea is doing BFS of paths instead of words.
    vector<vector<string>> ans;
    queue<vector<string>> paths;
    wordList.insert(endWord);
    paths.push({beginWord});
    int level = 1;
    int minLevel = INT_MAX;
    
    // The "visited" records all the visited nodes on this level
    // these words will never be visited again after this level 
    // and should be removed from wordList. This is guaranteed
    // by the shortest path.
    unordered_set<string> visited; 
    
    while (!paths.empty()) {
        vector<string> path = paths.front();
        paths.pop();
        if (path.size() > level) {
            //reach a new level
            for (string w : visited) wordList.erase(w);
            visited.clear();
            if (path.size() > minLevel)
                break;
            else
                level = path.size();
        }
        string last = path.back();
        // Find next words in wordList by changing
        // each element from 'a' to 'z'
        for (int i = 0; i < last.size(); ++i) {
            string news = last;
            for (char c = 'a'; c <= 'z'; ++c) {
                news[i] = c;
                if (wordList.find(news) != wordList.end()) {
                // Next word is in wordList, append this word to path.
                // Path will be reused in the loop, so copy a new path.
                    vector<string> newpath = path;
                    newpath.push_back(news);
                    visited.insert(news);
                    if (news == endWord) {
                        minLevel = level;
                        ans.push_back(newpath);
                    }
                    else
                        paths.push(newpath);
                }
            }
        }
    }
    return ans;
}
```


