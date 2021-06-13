---
layout: post
title: "Concurrent Systems: 03 "
date: 2021-02-03 13:01:20 +0300
description: Mutual Exclusion & Critical Section # Add post description (optional)
img:  software.jpg # Add image post (optional)(optional)
categories: [concurrent-systems]
icon: blogging.png
---

### Critical Sections
In concurrent programming, concurrent accesses to shared resources can lead to unexpected or erroneous behavior, so parts of the program where the shared resource is accessed need to be protected in ways that avoid the concurrent access. This protected section is the **critical section**

### Mutual Exclusion
Mutual exclusion is a property of concurrency control, which is instituted for the purpose of preventing race conditions. It is the requirement that one thread of execution never enters a critical section while a concurrent thread of execution is already accessing critical section, which refers to an interval of time during which a thread of execution accesses a shared resource.
 - Mutex can be implemented by use of locks.
 - contention may occur when consumer have to wait for lock. Dining Philosophers Problem: 5 Philosophers, 5 forks, round table.
 - Sleepable Locks
 - Spin Lock
 - Mutex is implemented using binary semaphore. (sem -> locking objects)

### Semaphore
Semaphore is simply a variable that is non-negative and shared between threads. This variable is used to solve the critical section problem and to achieve process synchronization in the multiprocessing environment. 
 - Binary Semaphore
 - Counting Semaphore
 - Producer Consumer problem implemented using Binary Semaphore for each producer & consumer.

#### Multi-Reader Single-Writer locks
- First semaphore is a mutual exclusion lock (mutex)
    - Any writer must wait to acquire this
- Second semaphore protects a reader count
    - Reader count incremented whenever a reader enters
    - Reader count decremented when a reader exits
    - First reader acquires mutex; last reader releases mutex

### Alternatives to Semaphores/locks
- **Conditional Critical Regions**
    - variables can be explicitly declared as 'shared'
    - code can be tagged as using those variables.
    - Compiler can automatically manages the underlying primitives of mutex 

- **Monitors**
    - Monitors are similar to CCRs (implicit mutual exclusion),but modify them in two ways
        - waiting is limited to explicit condition variables
        - – All related routines are combined together, along with initialization code, in a single construct
    - Idea is that only one thread can ever be executing ‘within’ the monitor
        - If a thread calls a monitor method, it will block (enqueue) if another thread is holding the monitor
    - Hence all methods within the monitor can proceed on the basis that mutual exclusion has been ensured
    - Java's `synchronized` primitive implements monitors.

- **Condition variables**
    - Condition variables are synchronization primitives that enable threads to wait until a particular condition occurs.
    - Monitors allow condition variables.
    ```java
    wait(condition-variable){
        // suspend thread and add it to the queue for CV, release monitor lock
    }
    signal(condition-variable){
        // if any threads queued on CV, wake one thread;
    }
    broadcast(condition-variable){
        // wake all threads queued on CV
    }
    ```

### Atomicity (Abortablity)
If a sequence of operations (e.g read-and-set) are made to occur as if one operation, we call them atomic.
- we can implement this by using atomic read-and-set
    - Atomic Compare and Sawp
    - Load Linked, Store Conditional

