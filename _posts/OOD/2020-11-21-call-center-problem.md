---
layout: post
title:  "Call Center Problem"
categories: [ Object-Oriented Design ]
tags: [ C++, OOD, Singleton Pattern ]
similar: [ OOD ]
featured: true
hidden: false
image: assets/images/callcenter.png
sidenav: OODProblems
excerpt: An object oriented design problem. Imagine you have a call center with three levels of employees, respondent, manager and director. An incoming telephone call must be first allocated to a respondent who is free.
---


<br/>

## Description

Imagine you have a call center with three levels of employees: respondent, manager and director. An incoming telephone call must be first allocated to a respondent who is free. If the respondent can't handle the call, he or she must escalate the call to a manager. If the manager is not free or not able to handle it, then the call should be escalated to a director. Design the classes and data structures for this problem. Implement a method **dispatchCall()** which assigns a call to the first available employee.


<br />

## C++ Implementation

Below is a complete C++ implementation of the call center problem. Put the code into separate files and run the Makefile at the end, the call center should be able to run.

#### Employee Class

For all three levels of employees, they have different work to be done, so we should first implement a base class *Employee* and then implement three derived class for the three levels respectively. In the *Employee* class, we should be able to check whether the current employee is available, and get and set this employee's level. When a call comes in, the employee should handle the call. If this employee can handle the call, then complete the call; otherwise, escalate the call. 

This is the implementation of the **employee.h** file.

```c
#ifndef __EMPLOYEE_H_
#define __EMPLOYEE_H_

enum EmployeeLevel { el_Respondent = 0, el_Manager = 1, el_Director = 2 };
EmployeeLevel nextEmployeeLevel(EmployeeLevel el);

// Forward Declaration
class Call;
class CallHandler;

class Employee {
private:
    Call *currentCall;
    EmployeeLevel employeeLevel;
public:
    Employee();
    ~Employee(){}

    bool isAvailable();
    EmployeeLevel getEmployeeLevel();
    void setEmployeeLevel(EmployeeLevel el);

    // Handle incoming calls dispatched by the callhandler
    void handleCall(Call *call);
    // Can handle this call, complete the call and assign a new call
    void completeCall();
    // Cannot handle this call, escalate the call and assign a new call
    void escalateCall();
    // Let the callhandler check whether there are waiting calls, if yes, handle the waiting calls
    void assignNewCall();
};

class Respondent: public Employee {
public:
    Respondent();
};

class Manager: public Employee {
public:
    Manager();
};

class Director: public Employee {
public:
    Director();
};

#endif /* __EMPLOYEE_H_ */

```

This is the implementation of the **employee.cpp** file.

```c
#include <iostream>
#include <vector>
#include <queue>
#include "employee.h"
#include "call.h"
#include "callhandler.h"

using namespace std;

EmployeeLevel nextEmployeeLevel(EmployeeLevel el) {
    switch (el) {
        case el_Respondent:
            return el_Manager;
        case el_Manager:
            return el_Director;
        case el_Director:
            return el_Director;
        default:
            return el_Respondent;
    }
}

Employee::Employee() {
}

bool Employee::isAvailable() {
    return (currentCall == nullptr);
}

EmployeeLevel Employee::getEmployeeLevel() {
    return employeeLevel;
}

void Employee::setEmployeeLevel(EmployeeLevel el) {
    employeeLevel = el;
}

void Employee::handleCall(Call *call) {
    currentCall = call;
    currentCall->setHandler(this);
    if (currentCall->getCallType() > employeeLevel) {
        escalateCall();
    } else {
        completeCall();
    }
}

void Employee::completeCall() {
    if (currentCall != nullptr) {
        currentCall->callComplete();
        currentCall = nullptr;
    }
    assignNewCall();
}

void Employee::escalateCall() {
    if (currentCall != nullptr) {
    CallHandler::getInstance()->escalateCall(currentCall, nextEmployeeLevel(employeeLevel));
        currentCall = nullptr;
    }
    assignNewCall();
}

void Employee::assignNewCall() {
    if (currentCall == nullptr) {
    CallHandler::getInstance()->assignCall(this);
    }
}

Respondent::Respondent() {
    setEmployeeLevel(el_Respondent);
}

Manager::Manager() {
    setEmployeeLevel(el_Manager);
}

Director::Director() {
    setEmployeeLevel(el_Director);
}
```

#### Call Class

The call represents a call from a user. A call has a call type, who handles it, and whether the call is complete.

This is the implementation of the **call.h** file.

```c
#ifndef __CALL_H_
#define __CALL_H_

#include "employee.h"

enum CallType { ct_Easy = 0, ct_Medium = 1, ct_Hard = 2 };

class Call {
private:
    static int callId;
  int currentId;
    CallType callType;
    Employee* handler;
    bool isComplete;
public:
    Call(CallType ct = ct_Easy);
  ~Call(){}

    CallType getCallType();
    void setCallType(CallType ct);

    void setHandler(Employee* h);

    bool getIsComplete();
    void setCallComplete();
    void callComplete();
};

#endif /* __CALL_H_ */
```

This is the implementation of the **call.cpp** file.

```c
#include <iostream>
#include <vector>
#include <queue>
#include "call.h"

using namespace std;

Call::Call(CallType ct) {
    callType = ct;
    isComplete = false;
  currentId = callId;
    callId ++;
}

CallType Call::getCallType() {
    return callType;
}

void Call::setCallType(CallType ct) {
    callType = ct;
}

void Call::setHandler(Employee* h) {
    handler = h;
}

bool Call::getIsComplete() {
    return isComplete;
}

void Call::setCallComplete() {
    isComplete = true;
}

void Call::callComplete() {
    setCallComplete();
    handler = nullptr;
    cout << "Call " << currentId << " (CallType=" << getCallType() << ") complete." << endl;
}
```


#### CallHandler Class

There should be a CallHandler class which would route the calls to the correct person. The CallHandler is implemented as a singleton class. All calls should be funneled first through it. The CallHandler should first set employees, and maintain a queue of calls. When a call comes in, it should dispatch the call to the first available employee. If the employee is not able to handle the call, the CallHandler should find an available employee at the next level.

This is the implementation of the **callhandler.h** file.

```c
#ifndef __CALLHANDLER_H_
#define __CALLHANDLER_H_

#include <vector>
#include <queue>
#include "employee.h"
#include "call.h"

class CallHandler {
private:
    // Singleton pattern
    static CallHandler *instance;

    int numOfRespondents;
    int numOfManagers;
    int numOfDirectors;

  std::vector<std::vector<Employee* > > employees;
  std::vector<Employee*> respondents;
  std::vector<Employee*> managers;
  std::vector<Employee*> directors;

  std::queue<Call*> callQueue;

    // Singleton pattern, so the constructor is private
    CallHandler();
    ~CallHandler(); 

public:
    static CallHandler* getInstance() {
        if (!instance) {
            instance = new CallHandler();
        }
        return instance;
    }

    // Get first available employee to handle the call
    Employee* getAvailableEmployee(EmployeeLevel el);

    void dispatchCall(Call *call);

    void escalateCall(Call *call, EmployeeLevel el);

    void assignCall(Employee *e);

};

#endif /* __CALLHANDLER_H_ */
```

This is the implementation of the **callhandler.cpp** file.

```c
#include <iostream>
#include <vector>
#include <queue>
#include "callhandler.h"

using namespace std;

CallHandler::CallHandler() {
    numOfRespondents = 10;
    numOfManagers = 5;
    numOfDirectors = 2;
    for (int i = 0; i < numOfRespondents; i ++) {
        respondents.push_back(new Respondent());
    }
    for (int i = 0; i < numOfManagers; i ++) {
        managers.push_back(new Manager());
    }
    for (int i = 0; i < numOfDirectors; i ++) {
        directors.push_back(new Director());
    }
    employees.push_back(respondents);
    employees.push_back(managers);
    employees.push_back(directors);
}

CallHandler::~CallHandler() {
    for (int i = 0; i < employees.size(); i ++) {
        for (int j = 0; j < employees[i].size(); j ++) {
            delete employees[i][j];
        }
    }
}

Employee* CallHandler::getAvailableEmployee(EmployeeLevel el) {
    for (int i = el; i < employees.size(); i ++) {
        for (int j = 0; j < employees[i].size(); j ++) {
            if (employees[i][j]->isAvailable())
                return employees[i][j];
        }
    }
    return nullptr;
}

void CallHandler::dispatchCall(Call *call) {
    Employee *employee = getAvailableEmployee(el_Respondent);
    if (employee == nullptr) {
        callQueue.push(call);
        return;
    }
    employee->handleCall(call);
    return;
} 

void CallHandler::escalateCall(Call *call, EmployeeLevel el) {
    Employee *employee = getAvailableEmployee(el);
    if (employee == nullptr) {
        callQueue.push(call);
        return;
    }
    employee->handleCall(call);
    return;
}

void CallHandler::assignCall(Employee *e) {
    if (callQueue.empty()) {
        return;
    }
    Call* c = callQueue.front();
    callQueue.pop();

    e->handleCall(c);
}
```

#### CallCenter 
The callcenter file is a test file to run the classes implemented above. Below is an example implementation of the **callcenter.cpp** file.

```c
#include <iostream>
#include <vector>
#include <queue>

#include "employee.h"
#include "call.h"
#include "callhandler.h"

using namespace std;


// Initialize pointer to zero so that it can be intialized in first call to getInstance
CallHandler *CallHandler::instance = 0;
// Initialize callID
int Call::callId = 0;

int main() {
    CallHandler *ch = CallHandler::getInstance();

  queue<Call*> callqueue;
  for (int i = 0; i < 5; i ++) {
    Call* c = new Call(ct_Easy);
    callqueue.push(c);
  }
  for (int i = 0; i < 8; i ++) {
    Call* c = new Call(ct_Medium);
    callqueue.push(c);
  }
  for (int i = 0; i < 5; i ++) {
    Call* c = new Call(ct_Hard);
    callqueue.push(c);
  }


  while (!callqueue.empty()) {
    Call* c = callqueue.front();
    callqueue.pop();

    ch->dispatchCall(c);
  }

    return 0;
}
```

#### Putting it All Together

For now, we should have a runnable call center. Use the following code as a **Makefile**.

```c
all: callcenter

callcenter: call.o callhandler.o employee.o callcenter.o
    g++ -o callcenter *.o

%.o: %.cpp
    g++ -o $@ -c $<
```

Then execute the following commands, we should see that the calls are handled.
```
make
./callcenter
```
