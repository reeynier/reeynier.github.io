---
layout: post
title: "Basic Calculator IV Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Hash Table, Math, String, Stack, Recursion ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 770. Given an expression such as expression = "e + 8 - a + 5" and an evaluation map such as 

---

<br />

## Description

LeetCode Problem 770.

Given an expression such as expression = "e + 8 - a + 5" and an evaluation map such as {"e": 1} (given in terms of evalvars = ["e"] and evalints = [1]), return a list of tokens representing the simplified expression, such as ["-1\*a","14"]
* An expression alternates chunks and symbols, with a space separating each chunk and symbol.
* A chunk is either an expression in parentheses, a variable, or a non-negative integer.
* A variable is a string of lowercase letters (not including digits.) Note that variables can be multiple letters, and note that variables never have a leading coefficient or unary operator like "2x" or "-x".

Expressions are evaluated in the usual order: brackets first, then multiplication, then addition and subtraction.
* For example, expression = "1 + 2 * 3" has an answer of ["7"].

The format of the output is as follows:
* For each term of free variables with a non-zero coefficient, we write the free variables within a term in sorted order lexicographically.
* For example, we would never write a term like "b\*a\*c", only "a\*b\*c".
* Terms have degrees equal to the number of free variables being multiplied, counting multiplicity. We write the largest degree terms of our answer first, breaking ties by lexicographic order ignoring the leading coefficient of the term.
* For example, "a\*a\*b\*c" has degree 4.
* The leading coefficient of the term is placed directly to the left with an asterisk separating it from the variables (if they exist.) A leading coefficient of 1 is still printed.
* An example of a well-formatted answer is ["-2\*a\*a\*a", "3\*a\*a\*b", "3\*b\*b", "4\*a", "5\*c", "-6"].
* Terms (including constant terms) with coefficient 0 are not included.
* For example, an expression of "0" has an output of [].

Example 1:
```
Input: expression = "e + 8 - a + 5", evalvars = ["e"], evalints = [1]
Output: ["-1*a","14"]
```

Example 2:
```
Input: expression = "e - 8 + temperature - pressure", evalvars = ["e", "temperature"], evalints = [1, 12]
Output: ["-1*pressure","5"]
```

Example 3:
```
Input: expression = "(e + 8) * (e - 8)", evalvars = [], evalints = []
Output: ["1*e*e","-64"]
```

Example 4:
```
Input: expression = "a * b * c + b * a * c * 4", evalvars = [], evalints = []
Output: ["5*a*b*c"]
```

Example 5:
```
Input: expression = "((a - b) * (b - c) + (c - a)) * ((a - b) + (b - c) * (c - a))", evalvars = [], evalints = []
Output: ["-1*a*a*b*b","2*a*a*b*c","-1*a*a*c*c","1*a*b*b*b","-1*a*b*b*c","-1*a*b*c*c","1*a*c*c*c","-1*b*b*b*c","2*b*b*c*c","-1*b*c*c*c","2*a*a*b","-2*a*a*c","-2*a*b*b","2*a*c*c","1*b*b*b","-1*b*b*c","1*b*c*c","-1*c*c*c","-1*a*a","1*a*b","1*a*c","-1*b*c"]
```

Constraints:
* 1 <= expression.length <= 250
* expression consists of lowercase English letters, digits, '+', '-', '\*', '(', ')', ' '.
* expression does not contain any leading or trailing spaces.
* All the tokens in expression are separated by a single space.
* 0 <= evalvars.length <= 100
* 1 <= evalvars[i].length <= 20
* evalvars[i] consists of lowercase English letters.
* evalints.length == evalvars.length
* -100 <= evalints[i] <= 100

<br />

## Sample C++ Code


```c
class Solution {
public:
    const map<pair<int, string>, int> evaluate(queue<map<pair<int, string>, int>>& es, queue<char>& os) {
        deque<map<pair<int, string>, int>> qe;
        deque<char> qo;
        
        if (es.size() == os.size()) {
            qe.push_back({ { {0, ""}, 0 } });
        } else {
            qe.push_back(es.front());
            es.pop();
        }
        
        const auto sorted = [](const pair<int, string>& k1, const pair<int, string>& k2) {
            map<string, int> cnts;
            string t;
            for (const char& c: k1.second) {
                if (c == '*') {
                    cnts[t]++;
                    t.clear();
                } else {
                    t += c;
                }
            }
            cnts[t]++;
            t.clear();
            for (const char& c: k2.second) {
                if (c == '*') {
                    cnts[t]++;
                    t.clear();
                } else {
                    t += c;
                }
            }
            cnts[t]++;
            t.clear();
            for (const auto&[k, v]: cnts)
                for (int i = 0; i < v; ++i)
                    if (!k.empty())
                        t += k + '*';
            
            if (!t.empty()) t.pop_back();
            return make_pair(k1.first + k2.first, t);
        };
        
        while (!es.empty()) {
            if (os.front() == '*') {
                map<pair<int, string>, int> p;
                for (const auto& [k1, v1]: qe.back())
                    for (const auto& [k2, v2]: es.front())
                        p[sorted(k1, k2)] += v1 * v2;
                        
                qe.pop_back();
                qe.push_back(p);
            } else {
                qo.push_back(os.front());
                qe.push_back(es.front());
            }
            es.pop();
            os.pop();
        }
        
        while (!qo.empty()) {
            auto e = qe.front();
            qe.pop_front();
            for (const auto& [k, v]: qe.front())
                qo.front() == '+' ? e[k] += v : e[k] -= v;
            qe.pop_front();
            qo.pop_front();
            qe.push_front(e);
        }
        
        return qe.front();
    }
    
    vector<string> basicCalculatorIV(string expression, vector<string>& evalvars, vector<int>& evalints) {
        expression += '!';
        unordered_map<string, int> known;
        int n(evalvars.size());
        for (int i = 0; i < n; ++i)
            known[evalvars[i]] = evalints[i];
        
        stack<queue<map<pair<int, string>, int>>> operands;
        stack<queue<char>> operators;
        string t;
        map<pair<int, string>, int> res;
        operands.push({});
        operators.push({});
        
        const auto is_num = [](const string& s) {
            for (const char& c: s)
                if (!isdigit(c))
                    return false;
            return true;
        };
        
        for (const char& c: expression) {
            if (c == ' ') continue;
            if (c == '(') {
                operands.push({});
                operators.push({});
            } else if (isalnum(c)) {
                t += c;
            } else {        
                if (!t.empty()) {
                    if (is_num(t)) {
                        operands.top().push({ { {0, ""}, stoi(t) } });
                    } else if (known.count(t)) {
                        operands.top().push({ { {0, ""}, known[t] } });
                    } else {
                        operands.top().push({ { {-1, t}, 1 } });
                    }
                }
                
                t.clear();
                if (c == ')' || c == '!') {
                    res = evaluate(operands.top(), operators.top());
                    operands.pop();
                    operators.pop();
                    if (c == '!') break;
                    operands.top().push(res);
                } else {
                    operators.top().push(c);
                }
            }
        }
        
        vector<string> ans(res.size());
        int i(0);
        for (const auto&[k, v]: res)
            if (v) 
                ans[i++] = to_string(v) + (k.second.empty() ? "" : "*" + k.second);
            
        ans.resize(i);
        return ans;
    }
};
```


