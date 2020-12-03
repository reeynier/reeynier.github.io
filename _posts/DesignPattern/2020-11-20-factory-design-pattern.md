---
layout: post
title:  "Factory Design Pattern"
categories: [ Design Pattern ]
tags: [ C++, Factory Pattern, Creational Pattern ]
similar: [ Design Pattern ]
featured: false
hidden: false
excerpt: The `factory` design pattern is a type of `creational pattern` to create an object.
---

<br />

The `factory` design pattern is a type of `creational pattern` to create an object. In `factory` pattern, we create object without exposing the creation logic to the client and refer to newly created object using a common interface.


<br />

## C++ Implementation

This example is a C++ implementation of the Shape example from [tutorialpoints](https://www.tutorialspoint.com/design_pattern/factory_pattern.htm){:target="_blank"}.


In this example, we are going to create a Shape interface and concrete classes implementing the Shape interface. 

```c
#include <iostream>
#include <string>
using namespace std;

class Shape {
public:
    virtual void draw() {}
};

class Rectangle : public Shape {
public:
    void draw() {
        cout << "Inside Rectangle draw() function." << endl;
    }
};

class Square : public Shape {
public:
    void draw() {
        cout << "Inside Square draw() function." << endl;
    }
};

class Circle : public Shape {
public:
    void draw() {
        cout << "Inside Circle draw() function." << endl;
    }
};

class ShapeFactory {
public:
    Shape* getShape(string shapeType) {
        if (shapeType == "Circle") {
            return new Circle();
        } else if (shapeType == "Rectangle") {
            return new Rectangle();
        } else if (shapeType == "Square") {
            return new Square();
        } else {
            return nullptr;
        }
    }
};

int main() {
    ShapeFactory* sf = new ShapeFactory();
    
    Shape* s1 = sf->getShape("Circle");
    s1->draw();

    Shape* s2 = sf->getShape("Rectangle");
    s2->draw();

    Shape* s3 = sf->getShape("Square");
    s3->draw();
}
```



