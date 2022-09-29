---
layout: post
title: "Parse Lisp Expression Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Hash Table, String, Stack, Recursion ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 736. You are given a string expression representing a Lisp-like expression to return the integer value of.

---

<br />

## Description

LeetCode Problem 736.

You are given a string expression representing a Lisp-like expression to return the integer value of.

The syntax for these expressions is given as follows.
* An expression is either an integer, let expression, add expression, mult expression, or an assigned variable. Expressions always evaluate to a single integer.
* (An integer could be positive or negative.)
* A let expression takes the form "(let v_1 e_1 v_2 e_2 ... v_n e_n expr)", where let is always the string "let", then there are one or more pairs of alternating variables and expressions, meaning that the first variable v_1 is assigned the value of the expression e_1, the second variable v_2 is assigned the value of the expression e_2, and so on sequentially; and then the value of this let expression is the value of the expression expr.
* An add expression takes the form "(add e_1 e_2)" where add is always the string "add", there are always two expressions e_1, e_2 and the result is the addition of the evaluation of e_1 and the evaluation of e_2.
* A mult expression takes the form "(mult e_1 e_2)" where mult is always the string "mult", there are always two expressions e_1, e_2 and the result is the multiplication of the evaluation of e1 and the evaluation of e2.
* For this question, we will use a smaller subset of variable names. A variable starts with a lowercase letter, then zero or more lowercase letters or digits. Additionally, for your convenience, the names "add", "let", and "mult" are protected and will never be used as variable names.
* Finally, there is the concept of scope. When an expression of a variable name is evaluated, within the context of that evaluation, the innermost scope (in terms of parentheses) is checked first for the value of that variable, and then outer scopes are checked sequentially. It is guaranteed that every expression is legal. Please see the examples for more details on the scope.

Example 1:
```
Input: expression = "(let x 2 (mult x (let x 3 y 4 (add x y))))"
Output: 14
Explanation: In the expression (add x y), when checking for the value of the variable x,
we check from the innermost scope to the outermost in the context of the variable we are trying to evaluate.
Since x = 3 is found first, the value of x is 3.
```

Example 2:
```
Input: expression = "(let x 3 x 2 x)"
Output: 2
Explanation: Assignment in let statements is processed sequentially.
```

Example 3:
```
Input: expression = "(let x 1 y 2 x (add x y) (add x y))"
Output: 5
Explanation: The first (add x y) evaluates as 3, and is assigned to x.
The second (add x y) evaluates as 3+2 = 5.
```

Example 4:
```
Input: expression = "(let x 2 (add (let x 3 (let x 4 x)) x))"
Output: 6
Explanation: Even though (let x 4 x) has a deeper scope, it is outside the context
of the final x in the add-expression.  That final x will equal 2.
```

Example 5:
```
Input: expression = "(let a1 3 b2 (add a1 1) b2)"
Output: 4
Explanation: Variable names can contain digits after the first character.
```

Constraints:
* 1 <= expression.length <= 2000
* There are no leading or trailing spaces in exprssion.
* All tokens are separated by a single space in expressoin.
* The answer and all intermediate calculations of that answer are guaranteed to fit in a 32-bit integer.
* The expression is guaranteed to be legal and evaluate to an integer.

<br />

## Sample C++ Code


```c
class Solution {
public:
    stringstream ss;
    unordered_map<string, vector<int>> var;
    int UNUSED = 1337;

    int evaluate(string s0) {
        string s;
        for(char c : s0) 
            s.append(c == '(' ? " ( " : c == ')' ? " ) " : string(1, c)); 
        ss = stringstream(s);
        return solve().second;
    }

    pair<string, int> solve() {
        string t; ss >> t;
        int ret;
        if (t == "(") { 
            string op; ss >> op;
            if (op == "add" || op == "mult") {
                auto op1 = solve(), op2 = solve();
                string discard; 
                ss >> discard;
                ret = op == "add" ? op1.second+op2.second : op1.second*op2.second;
            } else {
                vector<string> assign;
                pair<string, int> l, r;
                while (true) {
                    l = solve(), r = solve(), ret = l.second;
                    if (r.first == ")") 
                        break;
                    var[l.first].push_back(r.second);
                    assign.push_back(l.first);
                }
                for(string a : assign) 
                    var[a].pop_back();
            }
        }
        else if (t == ")") 
            ret = UNUSED;
        else if (isalpha(t.front())) 
            ret = var[t].empty() ? UNUSED : var[t].back();
        else 
            ret = stoi(t);
        return {t, ret};
    }   
};
```


