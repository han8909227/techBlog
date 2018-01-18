---
title: Interview Questions(CS fundamental)
date: 2018-01-10 23:58:12
tags:
- interview
- cs
- faq
categories:
- Technical interview prep
---



* What is the difference between a Thread and a Process?
> Tread is a path of execution within a process, a process can contain multiple threads.
> The treads within the same process run in a shared memory space, while process run in separate memory spaces. And treads are not independent of each other like process are.
<!--more-->

* What is Stack frame for Program?
> The set of values which is pushed into stack for one 'function call' is called 'stack frame'.
> The stack frame contains all information to save and restore the state of a program.
> The stack frame are allocated in a region of memory called the call stack
> Call Stack: ![alt text](https://upload.wikimedia.org/wikipedia/commons/thumb/d/d3/Call_stack_layout.svg/342px-Call_stack_layout.svg.png "Call Stack")

* When two threads access a code at the same time, what happens? How is it prevented?
> When two threads access a code at the same time, it may cause a 'race condition' where the values of variables may be unpredictable and vary depending on the timings of context switches of the process or threads.
> A 'race condition' occurs when the OS is trying to perform two or more operations at the same time.
> Thread synchronization can effectively eliminate 'race condition' by ensure two or more concurrent processes do not execute a particular code segment simultaneously

* How is map internally stored in C++?
> Map in C++ STL is implemented using a self balancing BST, usually Red Black Tree. This is to ensure O(log(n)) look up, insert and delete time.
