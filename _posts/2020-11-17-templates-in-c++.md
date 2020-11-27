---
layout: post
title:  "Templates in C++"
categories: [ C++ Concepts ]
tags: [ C++, Template, Function Template, Class Template ]
similar: [ C++ OOP ]
featured: false
hidden: false
excerpt: A `template` is a blueprint or formula for creating a generic class or a function.
---

<br />

A `template` is a blueprint or formula for creating a generic class or a function. The library containers like iterators and algorithms are examples of generic programming and have been developed using template concept.

There is a single definition of each container, such as vector, but we can define many different kinds of vectors for example, vector<int> or vector<string>.



## Function Template Example

Here is an example of a `function template` that returns the sum of two values.

```c
#include <iostream>
#include <string>

using namespace std;

template <typename T>
inline T Sum (T const& a, T const& b) { 
    return a + b; 
}

int main() {
    int i = 39, j = 20;
    cout << Sum(i, j) << endl;

    double f1 = 13.5, f2 = 20.7;
    cout << Sum(f1, f2) << endl;

    string s1 = "Hello", s2 = "World";
    cout << Sum(s1, s2) << endl;
}
```

The output of the above code is:
```
59
34.2
HelloWorld
```



<br />

## Class Template Example

Here is an example of a `class template` to define class Stack<> and implement generic method to push and pop the elements from the stack.

```c
#include <iostream>
#include <vector>

using namespace std;

template <class T>
class Stack {
private:
    vector<T> elems;
public:
    void push(T const& );
    void pop();
    T top() const;

    bool empty() const {
        return elems.empty();
    }
};

template <class T>
void Stack<T>::push (T const& elem) {
    elems.push_back(elem);
}

template <class T>
void Stack<T>::pop () {
    if (elems.empty()) {
        throw out_of_range("Stack<>::pop(): empty stack");
    }
    elems.pop_back();
}

template <class T>
T Stack<T>::top () const {
    if (elems.empty()) {
        throw out_of_range("Stack<>::top(): empty stack");
    }
    return elems.back();
}

int main() {
    try {
    	Stack<int> intStack;
    	Stack<string> stringStack;

    	intStack.push(7);
    	cout << intStack.top() << endl;

    	stringStack.push("hello");
    	cout << stringStack.top() << endl;
    	stringStack.pop();
    	stringStack.pop();
    } catch (exception const& ex) {
    	cerr << "Exception: " << ex.what() << endl;
    	return -1;
    }
}

```

The output of the above code is:
```
7
hello
Exception: Stack<>::pop(): empty stack
```









