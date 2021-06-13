---
layout: post
title: "Concurrent Systems: 01 "
date: 2021-02-03 13:01:20 +0300
description: Concurrent System. # Add post description (optional)
img:  software.jpg # Add image post (optional)(optional)
categories: [concurrent-systems]
icon: blogging.png
---
- **Concurrency** is about dealing with lots of things at once but **Parallelism** is about doing lots of things at once.

## Difference between Concurrrent and Distributed System
- Underlying primitives: **Shared Memory** vs **Message Passing**
- Distributed systems experience **communications failure**
- Distributed systems may experience **unbounded latency**
- Difficulty in syncing **distributed time**

## What is Concurrrency?
- Computers appear to do many things at once
    - E.g: running multiple programns on a laptop
    - E.g: writing back data buffered in memory to hard disk while the program continue to execute.
- In the first case, this may actually be an illusion
    - E.g: processes **time sharing** a single-cored CPU
- In the second case, there is a **true parallelism**
    - E.g: Direct Memory Access(DMA) transfers data between memory and I/O devices at the same time as the CPU executes code.
    - E.g: two CPU's execute code at the same time.

### Process
- Processes are instances of programs in execution
- OS unit of protection & resource allocation
- Has a virtual address space; and one or more threads

### Threads
- Threads are entities managed by the scheduler
- Represents an individual execution context
- A *thread control block* (TCB) holds the saved context (registers including stack pointer), scheduler info etc.
- Threads run in the **address spaces** of their process
- **Context switches** occur when the OS saves the state of one thread and restores the state of another.
- If a switch is between threads in different processes, then process state is also switched: eg: the address space.

### Concurrency with a single CPU
- With just one CPU, we can think concurrency as **interleaving** of different executions.
<pre>
-> Proc(A) -> OS  ->  Proc(B) -> OS ->  Proc(B) -> OS -> Proc(C) -> OS -> Proc(A)
              |                  |                 |                |
time->    timer interrupt     disk interrupt      system call     page fault
</pre>
- Concurrency is challenging since where execution will be interrupted and resumed is not known in advance.

**Process/OS concurrency**<br/>
- Process X runs for a while (until blocks or interrupted)
- OS runs for a while (e.g. does some TCP processing)
- Process X resumes where it left off

### Concurrency with a multiple CPUs
- Different threads can be executing on different CPU's of same process.
- Ordering of threads execution will be dynamic and are non-deterministic


