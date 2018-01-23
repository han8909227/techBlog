---
title: CS Fundamental(part 1 threads)
date: 2018-01-10 23:58:12
tags:
- interview
- cs
- faq
- threads
categories:
- Technical interview prep
---

# Technwical Questions
## What is the difference between a Thread and a Process?
> Tread is a path of execution within a process, a process can contain multiple threads.
> The treads within the same process run in a shared memory space, while process run in separate memory spaces. And treads are not independent of each other like process are.
<!--more-->

## What is Stack frame for Program?
> The set of values which is pushed into stack for one 'function call' is called 'stack frame'.
> The stack frame contains all information to save and restore the state of a program.
> The stack frame are allocated in a region of memory called the call stack
> Call Stack: ![alt text](https://upload.wikimedia.org/wikipedia/commons/thumb/d/d3/Call_stack_layout.svg/342px-Call_stack_layout.svg.png "Call Stack")

## When two threads access a code at the same time, what happens? How is it prevented?
> When two threads access a code at the same time, it may cause a 'race condition' where the values of variables may be unpredictable and vary depending on the timings of context switches of the process or threads.
> A 'race condition' occurs when the OS is trying to perform two or more operations at the same time.
> Thread synchronization can effectively eliminate 'race condition' by ensure two or more concurrent processes do not execute a particular code segment simultaneously

## How to synchronize thread?
> Java provides a way to create treads and synchronizing their task by using synchronized blocks. A synchronized block is marked with the synchronized keyword, a block is synchronized on some object and all blocks synchronized on the same
> object can only have one thread executing inside them at a time. All other threads trying to enter the block are blocked until the thread inside the synchronized block exit the block.

## Producer-Consumer solution using threads
>In computing, the producer–consumer problem (also known as the bounded-buffer problem) is a classic example of a multi-process synchronization problem. The problem describes two processes, the producer and the consumer, which share a common, fixed-size buffer used as a queue.
>
The producer’s job is to generate data, put it into the buffer, and start again.
At the same time, the consumer is consuming the data (i.e. removing it from the buffer), one piece at a time.
>
**Problem**
To make sure that the producer won’t try to add data into the buffer if it’s full and that the consumer won’t try to remove data from an empty buffer.
>
**Solution**
The producer is to either go to sleep or discard data if the buffer is full. The next time the consumer removes an item from the buffer, it notifies the producer, who starts to fill the buffer again. In the same way, the consumer can go to sleep if it finds the buffer to be empty. The next time the producer puts data into the buffer, it wakes up the sleeping consumer.
An inadequate solution could result in a deadlock where both processes are waiting to be awakened.
>
Implementation of Producer Consumer Class:
A LinkedList list – to store list of jobs in queue.
A Variable Capacity – to check for if the list is full or not
A mechanism to control the insertion and extraction from this list so that we do not insert into list if it is full or remove from it if it is empty.

>credit: geekforgeeks.org

## What is the life cycle of a thread? (Thread States)

>There are **five** states a thread can have (4 in Java no running state), they are:
**New**
When a new instance of thread is created, but before invoking it.
**Runnable**
After start() method is invoked, but the thread scheduler has not selected it to be the running thread
**Running**
The thread is running once the scheduler has slected it
**Non-Runnable(blocked)**
The thread is still alive, but currently not eligible to run
**Terminated**
The thread is dead when its run() method exists
![alt text](https://www.javatpoint.com/images/threadstates.jpg "Thread life cycle")


## How threads communicate with each other?
>Like the Producer-Consumer porblem where one thread is produceing data and other is consuming it, Java uses three methods called
wait(), notify() and notifyAll() they all belong to object class as final and must be used within a synchronized block only.
**wait()**- Tells the calling thread to give up the lock and go to sleep until some other thread enters the same monitor and calls notify()
**notify()**-Waks up one single thread that called wait() on the same object. But this does not give up a lock on a resource.
**notifyAll()**- Wakes up all the threads that called wait() on the same object