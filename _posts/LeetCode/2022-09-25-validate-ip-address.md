---
layout: post
title: "Validate IP Address Problem"
categories: [ Algorithm, Data Structure ]
tags: [ String ]
similar: [ String ]
featured: false
hidden: false
excerpt: LeetCode 468. Given a string queryIP, return "IPv4" if IP is a valid IPv4 address, "IPv6" if IP is a valid IPv6 address or "Neither" if IP is not a correct IP of any type.

---

<br />

## Description

LeetCode Problem 468.

Given a string queryIP, return "IPv4" if IP is a valid IPv4 address, "IPv6" if IP is a valid IPv6 address or "Neither" if IP is not a correct IP of any type.

A valid IPv4 address is an IP in the form "x_1.x_2.x_3.x_4" where 0 <= x_i <= 255 and x_i cannot contain leading zeros. For example, "192.168.1.1" and "192.168.1.0" are valid IPv4 addresses but "192.168.01.1", while "192.168.1.00" and "192.168@1.1" are invalid IPv4 addresses.

A valid IPv6 address is an IP in the form "x_1:x_2:x_3:x_4:x_5:x_6:x_7:x_8" where:
* 1 <= x_i.length <= 4
* x_i is a hexadecimal string which may contain digits, lower-case English letter ('a' to 'f') and upper-case English letters ('A' to 'F').
* Leading zeros are allowed in x_i.

For example, "2001:0db8:85a3:0000:0000:8a2e:0370:7334" and "2001:db8:85a3:0:0:8A2E:0370:7334" are valid IPv6 addresses, while "2001:0db8:85a3::8A2E:037j:7334" and "02001:0db8:85a3:0000:0000:8a2e:0370:7334" are invalid IPv6 addresses.

Example 1:
```
Input: queryIP = "172.16.254.1"
Output: "IPv4"
Explanation: This is a valid IPv4 address, return "IPv4".
```

Example 2:
```
Input: queryIP = "2001:0db8:85a3:0:0:8A2E:0370:7334"
Output: "IPv6"
Explanation: This is a valid IPv6 address, return "IPv6".
```

Example 3:
```
Input: queryIP = "256.256.256.256"
Output: "Neither"
Explanation: This is neither a IPv4 address nor a IPv6 address.
```

Example 4:
```
Input: queryIP = "2001:0db8:85a3:0:0:8A2E:0370:7334:"
Output: "Neither"
```

Example 5:
```
Input: queryIP = "1e1.4.5.6"
Output: "Neither"
```

Constraints:
* queryIP consists only of English letters, digits and the characters '.' and ':'.

<br />

## Sample C++ Code


```c
class Solution {
public:
    string validIPAddress(string IP) {
        return validIPv4(IP) ? "IPv4" : (validIPv6(IP) ? "IPv6" : "Neither");
    }
private:
    bool validIPv4(string IP) {
        if (count(IP.begin(), IP.end(), '.') != 3) {
            return false;
        }
        vector<string> parts = split(IP, '.');
        if (parts.size() != 4) {
            return false;
        }
        for (string part : parts) {
            if (part.empty() || part.size() > 3 || part.size() > 1 && part[0] == '0') {
                return false;
            }
            for (char c : part) {
                if (!isdigit(c)) {
                    return false;
                }
            }
            if (stoi(part) > 255) {
                return false;
            }
        }
        return true;
    }
    
    bool validIPv6(string IP) {
        if (count(IP.begin(), IP.end(), ':') != 7) {
            return false;
        }
        vector<string> parts = split(IP, ':');
        if (parts.size() != 8) {
            return false;
        }
        for (string part : parts) {
            if (part.empty() || part.size() > 4) {
                return false;
            }
            for (char c : part) {
                if (!isdigit(c) && (!isalpha(c) || toupper(c) > 'F')) {
                    return false;
                }
            }
        }
        return true;
    }
    
    vector<string> split(string s, char c) {
        vector<string> parts;
        string part;
        istringstream in(s);
        while (getline(in, part, c)) {
            parts.push_back(part);
        }
        return parts;
    }
};
```


