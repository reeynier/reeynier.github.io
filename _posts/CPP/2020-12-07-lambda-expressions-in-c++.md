---
layout: post
title:  "Lambda Expressions in C++"
categories: [ C++ Concepts ]
tags: [ C++, Lambda Expression ]
similar: [ C++ Basic ]
featured: false
hidden: false
excerpt: A lambda expression is a convenient way of defining an anonymous function object right at the location where it is invoked or passes as an argument to a function.
---

<br />

This post and the examples are from the [Microsoft C++ Documentation](https://docs.microsoft.com/en-us/cpp/cpp/lambda-expressions-in-cpp?view=msvc-160){:target="_blank"}. 



A lambda expression is a convenient way of defining an anonymous function object right at the location where it is invoked or passes as an argument to a function. 


#### Parts Of A Lambda Expression

A lambda expression usually contains the following parts:
1. Capture clause: It specifies which variables are captured, and whether the capture is by value or by reference.

2. Parameter list (optional): It resembles the parameter list for a function.

3. Mutable specification (optional): It enables the body of a lambda expression to modify variables that are captured by value.

4. Exception specification (optional): It indicates whether the lambda expression throws any exceptions, by using throw() / noexcept.

5. Return type (optional): It is automatically deduced by the compiler from the return expression, or is void if no return expression exists. It can also be specified with a trailing-return-type, which resembles the return part of an ordinary method or function. The trailing-return-type should include the keyword "->"" before the return type.

6. lambda body: It can contain anything that the body of an ordinary method or function can contain.

The general syntax of defining lambda expressions is as follows.

```
[capture clause](parameter_list) mutable exception -> return_type {
    Method Definition;
}
```

Below is an example of a simple lambda expression. The lambda expression is passed as the third argument to the std::sort() function.

```c
#include <algorithm>
#include <cmath>

void abssort(float* x, unsigned n) {
    std::sort(x, x + n, 
        // Lambda expression begins 
        [](float a, float b) {
            return (std::abs(a) < std::abs(b));
        } // end of lambda expression
    );
}
```


#### More About Capture Clause

Capture clause specifies which variables are captured, and whether the capture is by value or by reference. An empty capture clause, [], indicates that the body of the lambda expression accesses no variables in the enclosing scope. The clause [&] means all variables that you refer to are captured by reference, and the clause [=] means they are captured by value.

For example, if a lambda body accesses the external variable *total* by reference and the external variable *factor* by value, then the following capture classes are equivalent.
```
[&total, factor]   // total by reference, factor by value
[factor, &total]   // order does not matter
[&, factor]        // all by reference, factor is special (by value)
[factor, &]        // same as the above one, order does not matter
[=, &total]        // all by value, total is special (by reference)
[&total, =]        // same as the above one, order does not matter
```

Here is another example shows that if a capture clause includes a capture-default &, then no identifier in a capture of that capture clause can have the form & identifier (same for capture-default =).

```
[&, i]     // ok
[&, &i]    // error, i preceded by & when & is the default
[=, this]  // error, this when = is the default
[=, *this] // ok, captures this by value
[i, i]     // error, i repeated
```


#### Another Example

The following example contains a lambda expression that explicitly captures the variable n by value and implicitly captures the variable m by reference:

```c
#include <iostream>
using namespace std;

int main()
{
   int m = 0;
   int n = 0;
   [&, n] (int a) mutable { m = ++n + a; }(4);
   cout << m << endl << n << endl;
}
```

Because the variable n is captured by value, its value remains 0 after the call to the lambda expression. The mutable specification allows n to be modified within the lambda.




































































