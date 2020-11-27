---
layout: post
title:  "Weak_Ptr in C++"
categories: [ C++ Concepts ]
tags: [ C++, Smart Pointers, RAII, Weak_Ptr, Cyclic Reference, Weak Reference ]
similar: [ C++ Pointers ]
featured: false
hidden: false
excerpt: Sometimes an object must store a way to access the underlying object of a `shared_ptr` without causing the reference count to be incremented.
---

<br />

This article and the examples are from the [Microsoft C++ Documentation](https://docs.microsoft.com/en-us/cpp/cpp/how-to-create-and-use-weak-ptr-instances?view=msvc-160){:target="_blank"} and the [LearnCPP](https://www.learncpp.com/cpp-tutorial/15-7-circular-dependency-issues-with-stdshared_ptr-and-stdweak_ptr/){:target="_blank"}. 



Sometimes an object must store a way to access the underlying object of a `shared_ptr` without causing the reference count to be incremented. Typically, this situation occurs when you have cyclic references between `shared_ptr` instances. In that case, use `weak_ptr` to give one or more of the owners a weak reference to another `shared_ptr`. By using a `weak_ptr`, you can create a `shared_ptr` that joins to an existing set of related instances, but only if the underlying memory resource is still valid.


<br />

## Cyclic Reference

A `cyclic reference` is a series of references where each object references the next, and the last object references back to the first, causing a referential loop. The references do not need to be actual C++ references - they can be pointers, unique IDs, or any other means of identifying specific objects.


Consider the following example, where the shared pointers in two separated objects each point at the other object.

```c
#include <iostream>
#include <memory>
#include <string>

using namespace std;

class Person {
    string m_name;
    shared_ptr<Person> m_partner; // initially created empty

public:
    Person(const string &name): m_name(name) {
        cout << m_name << " created\n";
    }

    ~Person() {
        cout << m_name << " destroyed\n";
    }

    friend bool partnerUp(shared_ptr<Person> &p1, shared_ptr<Person> &p2) {
        if (!p1 || !p2) return false;
        p1->m_partner = p2;
        p2->m_partner = p1;

        cout << p1->m_name << " is now partnered with " << p2->m_name << endl;
        return true;
    }
};

int main() {
    auto lucy = make_shared<Person>("Lucy"); // create a Person named "Lucy"
    auto ricky = make_shared<Person>("Ricky"); // create a Person named "Ricky"

    partnerUp(lucy, ricky);
    return 0;
}
```

In this example, we dynamically allocate two Persons, "Lucy" and "Ricky" using make_shared(). "Lucy" and "Ricky" are destroyed at the end of main(). Then we partner them up. This sets the shared_ptr inside "Lucy" to point at "Ricky", and the shared_ptr inside "Ricky" to point at "Lucy". 

The output of this program is:
```
Lucy created
Ricky created
Lucy is now partnered with Ricky
```

This is not what we expect. No deallocation took place. What happened?

At the end of main(), the ricky shared pointer goes out of scope first. When that happens, ricky checks if there are any other shared pointers that co-own the Person "Ricky". There are Lucy's m_partner. Because of this, it does not deallocate "Ricky"; otherwise, Lucy's m_partner would end up as a dangling pointer. At this point, we now have one shared pointer to "Ricky" (Lucy's m_partner) and two shared pointers to "Lucy" (Lucy, and Ricky's m_partner).

Next the Lucy shared pointer goes out of scope, and the same thing happens. The shared pointer Lucy checks if there are anyother shared pointers co-owning the Person "Lucy". There are Ricky's m_partner, so Lucy is not deallocated. At this point, there is one shared pointer to "Lucy" (Ricky's m_partner) and one shared pointer to "Ricky" (Lucy's m_partner).

Then the program ends - and neither "Lucy" or "Ricky" have been deallocated. Essentially, "Lucy" ends up keeping "Ricky" from being destroyed, and "Ricky" ends up keeping "Lucy" from being destroyed.



<br/>

## Weak Pointer

The `weak_ptr` was designed to solve the cyclical ownership problem described above. A `weak_ptr` is an observer - it can observe and access the same object as a `shared_ptr` (or other `weak_ptrs`) but it is not considered an owner. When a shared pointer goes out of scope, it only considers whether other `shared_ptr` are co-owning the object, and `weak_ptr` does not count.

The downside of `weak_ptr` is that `weak_ptr` are not directly usable (they have no operator ->). To use a `weak_ptr`, you must first convert it into a `shared_ptr`. Then you can use the `shared_ptr`. To convert a `weak_ptr` into a `shared_ptr`, you can use the lock() member function.

Let's rewrite the above example with weak pointers.

```c
#include <iostream>
#include <memory>
#include <string>

using namespace std;

class Person {
    string m_name;
    weak_ptr<Person> m_partner; // This is now a weak_ptr

public:
    Person(const string &name): m_name(name) {
        cout << m_name << " created\n";
    }

    ~Person() {
        cout << m_name << " destroyed\n";
    }

    friend bool partnerUp(shared_ptr<Person> &p1, shared_ptr<Person> &p2) {
        if (!p1 || !p2) return false;
        p1->m_partner = p2;
        p2->m_partner = p1;

        cout << p1->m_name << " is now partnered with " << p2->m_name << endl;
        return true;
    }

    // Use lock() to convert a weak_ptr to a shared_ptr
    const shared_ptr<Person> getPartner() const { return m_partner.lock(); }

    const string& getName() const { return m_name; }
};

int main() {
    auto lucy = make_shared<Person>("Lucy"); // create a Person named "Lucy"
    auto ricky = make_shared<Person>("Ricky"); // create a Person named "Ricky"

    partnerUp(lucy, ricky);

    auto partner = ricky->getPartner(); // get shared_ptr to Ricky's partner
    cout << ricky->getName() << "'s partner is: " << partner->getName() << '\n';

    return 0;
}
```

The output of the above example is:
```
Lucy created
Ricky created
Lucy is now partnered with Ricky
Ricky's partner is: Lucy
Ricky destroyed
Lucy destroyed
```

Now when Ricky goes out of scope, it sees that there are no other shared_ptr pointing at "Ricky" (the weak_ptr from "Lucy" doesn't count). Therefore, it will deallocate "Ricky". The same occurs for Lucy.

We don't have to worry about circular dependencies with shared_ptr variable "partner" since it's just a local variable inside the function. It will eventually go out of scope at the end of the function and the reference count will be decremented by 1.







