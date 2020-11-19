---
layout: post
title:  "Friend Class and Function in C++"
categories: [ C++ Concepts ]
tags: [ C++, Friend Class, Friend Function ]
similar: [ C++ OOP ]
featured: false
hidden: false
---

<br />


## Friend Class

A `friend class` can access private and protected members of other class in which it is declared as friend.

Here is an example of add a class as a friend class. Class B can access the private member "elem" in Class A.
```c
class A {
private:
    int elem;
    friend class B;
};
```


<br />

## Friend Function

A `friend function` can be given special grant to access private and protected members. A `friend function` can be a method of another class, or a global function.

```c
class A {
private:
    int elem;
    friend int B::search();
};
```

In this example, only the search() function in class B can access class A's internal members.

Friendship is not mutual. If class A is a friend of B, B does not become a friend of A automatically. Friendship is not inherited. The concept of friends is not in Java.







