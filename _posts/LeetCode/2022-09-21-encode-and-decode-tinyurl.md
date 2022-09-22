---
layout: post
title: "Encode And Decode TinyURL Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Hash Table, String, Design, Hash Function ]
similar: [ Design ]
featured: false
hidden: false
excerpt: LeetCode 535. TinyURL is a URL shortening service where you enter a URL such as

---

<br />

## Description

LeetCode Problem 535.

TinyURL is a URL shortening service where you enter a URL such as https://leetcode.com/problems/design-tinyurl and it returns a short URL such as http://tinyurl.com/4e9iAk. Design a class to encode a URL and decode a tiny URL.

There is no restriction on how your encode/decode algorithm should work. You just need to ensure that a URL can be encoded to a tiny URL and the tiny URL can be decoded to the original URL.

Implement the Solution class:
* Solution() Initializes the object of the system.
* String encode(String longUrl) Returns a tiny URL for the given longUrl.
* String decode(String shortUrl) Returns the original long URL for the given shortUrl. It is guaranteed that the given shortUrl was encoded by the same object.

Example 1:
```
Input: url = "https://leetcode.com/problems/design-tinyurl"
Output: "https://leetcode.com/problems/design-tinyurl"
Explanation:
Solution obj = new Solution();
string tiny = obj.encode(url); // returns the encoded tiny url.
string ans = obj.decode(tiny); // returns the original url after deconding it.
```

Constraints:
* 1 <= url.length <= 10^4
* url is guranteed to be a valid URL.

<br />

## Sample C++ Code


```c
class Solution {
public:
    unordered_map<string, string> codeDB, urlDB;
    const string chars = "0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz";
    
    string getCode() {
        string code = "";
        for (int i = 0; i < 6; i++) 
            code += chars[rand() % 62];
        return "http://tinyurl.com/" + code;
    }
    
    string encode(string longUrl) {
        if (urlDB.find(longUrl) != urlDB.end()) 
            return urlDB[longUrl];
        string code = getCode();
        while (codeDB.find(code) != codeDB.end()) 
            code = getCode();
        codeDB[code] = longUrl;
        urlDB[longUrl] = code;
        return code;
    }

    string decode(string shortUrl) {
        return codeDB[shortUrl];
    }
};

// Your Solution object will be instantiated and called as such:
// Solution solution;
// solution.decode(solution.encode(url));
```


