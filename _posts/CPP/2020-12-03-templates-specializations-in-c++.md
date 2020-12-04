---
layout: post
title:  "Template Specializations in C++"
categories: [ C++ Concepts ]
tags: [ C++, Template, Template Specialization, Partial Specialization ]
similar: [ C++ OOP ]
featured: false
hidden: false
excerpt: A `template specialization` is a separate definition in which the types or values of one or more template parameters are specified.
---

<br />

It is not always possible to write a single template that is best suited for every possible template argument with which the template might be instantiated. Below is an example:

```
template <typename T>
int compare(const T &v1, const T &v2) {
    if (v1 < v2) return -1;
    if (v2 < v1) return 1;
    return 0;
}
```

If we call this template definition on two const char\* arguments, the function compares the pointer values. The function compares the relative positions in memory of these two pointers, but not the contents of the arrays to which the pointers point. To be able to use this function for character arrays, we need to provide a specialized definition for C-style strings. The specialized versions of this template is transparent to users.




#### Specializing A Function Template


A `template specialization` is a separate definition in which the types or values of one or more template parameters are specified. Here is a specialization definition of the above compare function when the template parameter type is bound to const char\*.

```
// special version of compare to handle const char*
template <>
int compare<const char*> (const char* const &v1, const char* const &v2) {
    return strcmp(v1, v2);
}
```

When we call the compare function and pass it two character pointers, the compiler will call our specialized version.
```
const char *cp1 = "world", *cp2 = "hi";
int i1, i2;
compare(cp1, cp2);  // call the specialized version
compare(i1, i2);    // call the generic version
```



#### Specializing A Class Template

If we consider the Stack example in the [class template post]({% post_url CPP/2020-11-17-templates-in-c++ %}), we have the similar problem as in the compare function. One way to provide the right behavior for Stack of C-style strings is to define a specialized version of the entire class for const char\*.

```
template<> class Stack<const char*> {
private:
    vector<string> elems;
public:
    void push(const char* const &elem) {
        elems.push_back(elem);
    }
    void pop() {
        if (elems.empty()) {
            throw out_of_range("Stack<>::pop(): empty stack");
        }
        elems.pop_back();
    }
    string top() const {
        if (elems.empty()) {
            throw out_of_range("Stack<>::top(): empty stack");
        }
        return elems.back();
    }
    bool empty() const {
        return elems.empty();
    }
};
```



#### Class-Template Partial Specializations

If a class template has more than one template parameter, we might want to specialize some but not all of the template parameters. We can do so using a class template `partial specialization`. A class template partial specialization is itself a template. 

```
template <class T1, class T2>
class some_template {
    // ...
};

// partial specialization: fixes T2 as int and allows T1 to vary
template <class T1>
class some_template<T1, int> {
    // ...
}
```





