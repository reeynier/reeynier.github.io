---
layout: post
title:  "Singleton Design Pattern"
categories: [ Design Pattern ]
tags: [ C++, Singleton Pattern, Creational Pattern ]
similar: [ Design Pattern ]
featured: false
hidden: false
---

<br />

The `singleton` design pattern is a type of `creational pattern` to create an object. This pattern involves a single class which is responsible to create an object while making sure that only **single** object gets created. This class provides a way to access its only object which can be accessed directly without need to instantiate the object of the class.


<br />

## C++ Implementation

The `singleton` design pattern is useful when exactly one object is needed to coordinate actions across the system. For example, if you are using a logger, that writes logs to a file, you can use a singleton class to create such a logger. The following code is an example singleton class.

```c
#include <iostream>

using namespace std;

class Singleton {
    // The instance must be static to ensure there is only one instance globally
    static Singleton *instance;
    int data;

    // The constructor is private so that no objects can be created
    Singleton() {
        data = 0;
    }

public:
    // The getInstance function must be static
    // Otherwise, there will be a chicken-and-egg problem
    // (We do not have an instance, but we are using an instance member function to get an instance.)
    // Static function is not a member function
    // It does not belong/bind to an instance, it belongs to the class
    // So there will no chicken-and-egg problem
    static Singleton *getInstance() {
        // Check if instance is null, if so create a new instance
        // Otherwise, just return the existing instance
        // This ensures that only one instance exists globally
        if (!instance) {
            instance = new Singleton;
        }
        return instance;
    }

    int getData() {
        return this->data;
    }

    void setData(int data) {
        this->data = data;
    }

};

// Initialize pointer to zero so that it can be initialized in first call to getInstance
Singleton *Singleton::instance = 0;

int main() {
    Singleton *s = s->getInstance();
    cout << s->getData() << endl;
    s->setData(100);
    cout << s->getData() << endl;
    return 0;
}
```

The output of the above program is:
```
0
100
```

There are four things that we need to be careful when writing a `singleton` class:
1. The getInstance function should be static.
2. In the getInstance function, we need to check whether the instance is NULL.
3. The instance should also be static.
4. The constructor should private.





