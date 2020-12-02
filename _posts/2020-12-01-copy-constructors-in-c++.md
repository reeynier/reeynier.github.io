---
layout: post
title:  "Copy Constructors in C++"
categories: [ C++ Concepts ]
tags: [ C++, Copy Constructors ]
similar: [ C++ OOP ]
featured: false
hidden: false
excerpt: The constructor that takes a single parameter that is a reference to an object of the class type itself is called the copy constructor.
---

<br />

## The Copy Constructor

The constructor that takes a single parameter that is a (usually *const*) reference to an object of the class type itself is called the `copy constructor`. 


#### When Copy Constructors Are Used

The copy constructor can be implicitly invoked by the complier. The copy constructor is used in following cases.

* Explicitly or implicitly initialize one object from another of the same type.

C++ supports two forms of initialization: direct and copy. Direct initialization directly invokes the constructor matched by the arguments. Copy initialization first use the constructor to create a temporary object, it then uses the copy constructor to copy that temporary object into the one we are creating.

```
// copy initialization: first create a temporary by invoking the string constructor, 
// then uses the string copy construcor to initialize null_book as a copy of that temporary
string null_book = "9-999-99999-9";  

// direct initialization
string dots(10, '.');  

// copy initialization: the default constructor creates a temporary object, 
// which is then used by the copy constructor to initialize empty_copy
string empty_copy = string();  

// direct initialization
string empty_direct;  
```
* Copy an object to pass it as an argument to a function.

```
bool isShorter(string s1, string s2);
```

* Copy an object to return it from a function.

```
// copy constructor used to copy the return value;
// parameters are references, so they aren't copied
string make_plural(size_t, const string&, const string&);
```

* Initialize the elements in a sequential container.

```
// default string constructor and five string copy constructors invoked
vector<string> svec(5);
```

* Initialize elements in an array from a list of element initializers.

```
Sales_item primer_eds[] = { string("0-201-16487-6"), 
                            string("0-201-54848-8"), 
                            string("0-201-82470-1"),
                          };
```

#### Define Our Own Copy Constructor

For many classes, the default copy constructor does exactly the work that is needed. However, some classes must take control of what happens when objects are copied. Such classes often have a data member that is a pointer or that represents another resource that is allocated in the constructor. In these cases, the copy constructor must be defined.


```c
#include <iostream>

using namespace std;

class NoName {
private:
    string *pstring;
    int i;
    double d;
public:
    NoName() {   // constructor
    	cout << "Constructor;" << endl;
    	pstring = new string();
    	i = 0;
    	d = 0;
    }  
    NoName(const NoName& nn) {   // copy constructor
    	cout << "Copy Constructor;" << endl;
        pstring = new string();
        *pstring = *nn.pstring;
        i = nn.i;
        d = nn.d;
    }
    ~NoName() {   // destructor
    	cout << "Destructor;" << endl;
    	delete pstring;
    }
    void setPstring(string &s) {
        *pstring = s;
    }
    void display() {
    	cout << *pstring << endl;
    }
};

int main() {
    NoName n1;
    string s = "hello";
    n1.setPstring(s);
    NoName n2 = n1;
    n1.display();
    n2.display();
}
```

The output of the above code is:
```
Constructor;
Copy Constructor;
hello
hello
Destructor;
Destructor;
```

However, if we comment out the copy constructor, the output of the above code will be:
```
Constructor;
hello
hello
Destructor;
Destructor;
free(): double free detected in tcache 2
Aborted
```

This is because if there is no copy constructor, when we assign n1 to n2, the pstring pointer in n2 will point to the same object as the pstring in n1. So both of n1 and n2's destructors are trying to destroy the same object. If we add the copy constructor, we will allocate a new string pointer in n2. The two destructors will destroy its own string pointer object.































