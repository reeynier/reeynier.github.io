---
layout: post
title:  "Lvalue References in C++"
categories: [ C++ Concepts ]
tags: [ C++, Reference, Lvalue Reference, Rvalue Reference ]
similar: [ C++ Basic ]
featured: false
hidden: false
excerpt: An `lvalue reference` is another name of an object. An lvalue reference declaration consists of an optional list of specifiers followed by a reference declarator.
---

<br />

This post and the examples are from the [Microsoft C++ Documentation](https://docs.microsoft.com/en-us/cpp/cpp/lvalue-reference-declarator-amp?view=msvc-160){:target="_blank"}. 



An `lvalue reference` is another name of an object. An lvalue reference declaration consists of an optional list of specifiers followed by a reference declarator. A reference must be initialized and cannot be changed.

An object whose address can be converted to a pointer type can also be converted to the similar reference type. For example, any object whose address can be converted to type **char \*** can also be converted to **char &**.


Note that the reference declaration is **not** the same as the `address-of operator`. When the & identifier is preceded by a type (e.g. int, char), it is used as a reference declaration. When the & identifier is not preceded by a type, it is as the address-of operator.

Below is an example of using the reference to a Course object. 

```c
#include <iostream>
using namespace std;

struct Course
{
    char* Name;
    char* Time;
};

int main()
{
   // Declare a Course object.
   Course myCourse;

   // Declare a reference to the Course object.
   Course& rCourse = myCourse;

   // Set the fields of the Course object.
   // Updating either variable changes the same object.
   myCourse.Name = "Operating System";
   rCourse.Time = "Wednesdays";

   // Print the fields of the Person object to the console.
   cout << rCourse.Name << " is on " << myCourse.Time << endl;
}
```

The output is as follows. Because rFriend is a reference to myFriend, updating either variable changes the same object.

```
Operating System is on Wednesdays
```
























































