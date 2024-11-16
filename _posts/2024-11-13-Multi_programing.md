---
title: C++ Multi-thread Programming
tags:
  - C++
  - Multithread
---

Multi-thread processor is a processor which has process units over than 2.
The process unit could be a processor chip with independent CPU or a CPU named as core.
The multi-processor is widely used recently.
Thus, the multithread programming is latest technology.

## Concept of multi-thread programming

The speed of CPU has a limitation due to power consumption and heat.
If the CPUs works in parallel, then the operating duration would be shorter than previous.
Now, the dual and quadra core process is universal.
Furthermore, 12, 18 and 18 core processor are introduced.

GPU which is processor for graphic card are quitely parallelized.
The high-performed graphic card has over than 4000 cores.
The graphic card is used not only to play a game, but also to calculate mathematical operations and research a scientific phenomena.

From C++11, the standard multithread library is included. 
The current C++ defines API for CPU except for GPU.
But it can be support GPU soon.

The profits of multi-threading are two.
First, the overall performance increases.
The given work is divided to small problems.
And the problems can be operated in parallel.
Second, the responce speed of UI increases.
An operation taking a long time run on background.

It isn't correct that all problem can be solved in parallel.
But it is profit that a part of work is operated in parallel.
A race condition, dead lock, tearing, false-sharing should be avoided.

### Race condition

The race condition occurs when several thresds access to shared resource simultaneously.
The race condition about memory, especially, is called as data race.
Previous architectures such like PDP-11 or VAX provide the instruction like INC which runs atomically.
But INC provided by the latest x86 architecture isn't atomic anymore.
The results can be differed because other instruction can run during processing INC.

### Tearing
It is special case of data race.
Tearing can be divided to torn read and torn write.
If any thread use a part of data and other thread read this data, then the values of each threads are differed.
It is called as torn read.
And the results performed by two thread are also different when a thread write a part of data and other write another part of data.
It is named as torn write.

### Dead Lock
A dead lock is a condition in which multiple threads are waiting for another thread to complete its work.
Thread 1 wait that Thread 2 complete its work and Thread 2 also wait that Thread 1 complete its work simultaneously.
It means they wait permanantly each other.

To avoid dead lock, all threads acquire resources in a certain order.
It is good to made a mechanism breaking out of dead lock.
One way is to place a time limit on operations that request source access.

However, it is best to avoid for the dead lock to occur.
Functions such like std::lock() and std::try_lock() is used to secure or request the right of several resource.

### False-sharing
A cache is processed by a unit of cache line.
To write data to a cache line, the cache line must be locked.
The performance can decreases when locking to cache line if the data structure isn't well-made.
Since C++17, the constant, `hardware_destructive_interference_size`, is added in `<new>` header file to write codes transplantable.
It provides at least offset for two objects not to share same cache line.
It is okay to use this value and `alignas` keyword for aligning data properly.

## Thread
Thread is created with C++ thread library in `<thread>` header file.
There are three ways to determine what a thread is doing:
1. Expressing as `operator()` of function objects
2. Assigning as Lambda expression
3. Assigning as member function in the instances of specific class

### Making thread using function pointer
Functions of the `std::thread` class provided by the C++ standard can take as many parameters as desired.