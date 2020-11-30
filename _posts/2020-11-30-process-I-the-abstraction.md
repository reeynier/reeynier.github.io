---
layout: post
title:  "Process I: The Abstraction"
categories: [ Operating System ]
tags: [ Process ]
similar: [ Process ]
featured: false
hidden: false
excerpt: How can the OS provide the illusion of nearly-endless supply of said CPUs.
---

<br />

This post is adapted from Professor Remzi H. Arpaci-Dusseau and  Professor Andrea C. Arpaci-Dusseau's [OSTEP](http://pages.cs.wisc.edu/~remzi/OSTEP/){:target="_blank"} book, Chapter 4.

## The Abstraction

It is often the case that one wants to run more than one program at once. A typical system may be seemingly running tens or even hundreds of processes at the same time. So the challenge is: how to provide the illusion of many CPUs? Although there are only a few physical CPUs available, how can the OS provide the illusion of nearly-endless supply of said CPUs?

The OS creates this illusion by `virtualizing` the CPU. By running one process, then stopping it and running another and so forth, the OS can provide the illusion that many virtual CPUs exist when in fact there is only one physical CPU (or a few). This technique, known as `time sharing` of the CPU, allows users to run as many concurrent processes as they would like. 


#### Process Components

The abstraction provided by the OS of a **running program** is called a `process`. The question is what constitutes a process? What a program can read or update when it is running? At any given time, what parts of the machine are important to the execution of this program? We need to understand the process's machine state.

One component of machine state that comprises a process is its *memory*. The running program's instructions and data are in memory. So the memory that the process can address (called `address space`) is part of the process.

Another component is the *registers*. Many instructions read or update registers, so the registers are important to the execution of the process. These registers also include some special registers, such as the `program counter (PC)` (or `instruction pointer, IP`), `stack pointer`, `frame pointer`, and so on.

The last component is the *I/O information*. The I/O information includes a list of the files the process currently has opened.


#### Process APIs

The OS provides some interfaces to create and control the processes.

`Create`: An interface to create new processes to run the program you have indicated.

`Destroy`: An interface to destroy processes. If a process does not exit by themselves, it is useful to prvoide an interface to the user to kill or halt it.

`Wait`: An interface to wait for a process to stop running.

`Miscellaneous Control`: For example, an interface to suspend a process (stop it from running for a while), and an interface to resume it (continue it running).

`Status`: An interface to get some status information about a process.


#### Process Creation

One question we have is how programs are transformed into processes (running programs). Specifically, how does the OS get a program up and running? How does process creation work?

Programs initially are on `disk`. To run a program, the OS must load its code and data into memory. Modern OSes loads processes lazily. They only load pieces of code or data if they are needed during program execution. Once the code and static data are loaded into memory, the OS need to allocate some memory for the program's `run-time stack`. C programs use the stack for local variables, function parameters, and return addresses; the OS allocates this memory and gives it to the process. The OS also allocates some memory for the program's `heap`. C program use the heap for dynamically-allocated data. The OS also does some I/O related initialization. Finally, the OS will jump to the main() routine and transfer control of the CPU to the newly-created process. The progarm then begins its execution.


#### Process States

After creation, a process can be in different states at a given time. In a simplified view, a process can be in one of three states.

`Running`: In the running state, a process is running on a process and executing instructions.

`Ready`: In the ready state, a process is ready to run but for some reason the OS has chosen not to run it at the given moment.

`Blocked`: In the blocked state, a process has performed some kind of operation (e.g. initiate an I/O request to a disk) that makes it not ready to run until some other events take place.














































