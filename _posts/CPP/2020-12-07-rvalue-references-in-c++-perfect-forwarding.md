---
layout: post
title:  "Rvalue References in C++: Perfect Forwarding"
categories: [ C++ Concepts ]
tags: [ C++, Reference, Lvalue Reference, Rvalue Reference ]
similar: [ C++ Reference ]
featured: false
hidden: false
excerpt: Perfect forwarding reduces the need for overloaded functions and helps avoid the forwarding problem.
---

<br />

This post and the examples are from the [Microsoft C++ Documentation](https://docs.microsoft.com/en-us/cpp/cpp/rvalue-reference-declarator-amp-amp?view=msvc-160){:target="_blank"}. 



The `rvalue references` enable us to distinguish an lvalue from an rvalue (see [this post]({% post_url CPP/2020-12-07-value-categories-in-c++ %}) for more detail about value categories). In this post, we show how rvalue references support the implementation of perfect forwarding.


#### Perfect Forwarding

The `perfect forwarding` reduces the need for overloaded functions and helps avoid the forwarding problem. The `forwarding problem` can occur when we write a generic function that takes references as parameters, and this function passes (or `forwards`) these parameters to another function.

For example, if the generic function takes a parameter of type *const T&*, then the called function cannot modify the value of that parameter. If the generic function takes a parameter of type *T&*, then the function cannot be called by using an rvalue (such as a temporary object or integer literal). 

To solve the forwarding problem, we can provide **overloaded** versions of the generic function that take both *T&* and *const T&* for each of its parameters. However, this will increase the number of overloaded functions exponentially with the nubmer of parameters. 

Rvalue references enable us to write one version of a function that accepts arbitrary arguments and forwards them to another function as if the other function had been called directly.

#### An Example

Let's consider the following example.

```c
#include <iostream>

template <typename T,typename Arg>
T create(Arg& a){
  return T(a);
}


int main(){
  // Lvalues
  int five = 5;
  int myFive = create<int>(five);

  // Rvalues
  int myFive2 = create<int>(5);
}
```

If we compile this program, we will get an error. This is because in line 15, we are passing an rvalue parameter to the function create while this function only takes an lvalue reference parameter that is modifiable. 

To solve this problem, we can overload the create method for a constant lvalue reference.

```c
#include <iostream>

template <typename T,typename Arg>
T create(Arg& a){
  return T(a);
}

template <typename T,typename Arg>
T create(const Arg& a){
  return T(a);
}

int main(){
  // Lvalues
  int five = 5;
  int myFive = create<int>(five);

  // Rvalues
  int myFive2 = create<int>(5);
}
```

This time, we can get the expected result. However, as the number of parameters increase, the number of functions we need to write increase exponentially.


Thus, we can use the rvalue as an universal reference to solve this problem. The program looks like below:

```c
#include <iostream>

template <typename T,typename Arg>
T create(Arg&& a){
  return T(std::forward<Arg>(a));
}


int main(){
  // Lvalues
  int five = 5;
  int myFive = create<int>(five);

  // Rvalues
  int myFive2 = create<int>(5);
}
```

The `universal reference` (in line 4 in this example) can be lvalues and rvalues, depending on the context. The forward function (in line 5 in this example) returns the underlying types of the parameters (either lvalues or rvalues). In this way, the create function can forward its parameter to the appropriate class constructor.




































