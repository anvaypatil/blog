---
layout: post
title: "Concurrent Systems: 02 "
date: 2021-02-03 13:01:20 +0300
description: Threads & Processes. # Add post description (optional)
img:  software.jpg # Add image post (optional)(optional)
categories: [concurrent-systems]
icon: blogging.png
---

## Multiple threads within a process
- A single-threaded process has **code**, a
**heap**, a **stack**, **registers**
- **Threads** have their own
registers and stacks
    - `program counters` per thread
    - `stack pointers` per thread
- **Heap** and **global variables** arae shared between threads
- Access to another thread's stack is possible in some programing langugages - are but is not a paradigm

<br/>

### CPU scheduling
 The basic difference between **preemptive** and **non-preemptive scheduling** is that in preemptive scheduling the CPU is allocated to the processes for the limited time. While in Non-preemptive scheduling, the CPU is allocated to the process till it terminates or switches to waiting state.

## 1:N user-level threading
- **Kernel** only knows about (and schedules) processes
- A **userspace library** implements threads, context switching, scheduling, synchronisation, … E.g: the JVM or any threading library
- *Advantages*: Lightweight creation/termination + context switch; application-specific scheduling; OS independence.
- *Disadvantages*: Awkward to handle blocking system calls or page faults, preemption; cannot use multiple CPUs

## 1:1 kernel-level threading
- **Kernel** provides threads directly, By default, a process has one thread but can create more via system calls.
- **Kernel** implements threads, thread context switching, scheduling etc.
- **Userspace** thread library **1:1** maps **user threads** to **kernel threads**
- *Advantages*: 
    - Handles preemption,, blocking syscalls
    - Straightforeward to use multiple CPUs
- *Disadvantages*:
    - Higher overhead (trap to kernel); less flexible; less portable.
- Model of choice accross major OSes; Windows, Linux, MacOX, FreeBSD etc

## M:N hybrid threading
- M:N threads mapping, **scheduler activations**.
- **Scheduler activations** are a threading mechanism, when implemented in an operating system's process scheduler, provide kernel-level thread functionality with user-level thread flexibility and performance.
- **Kernel** exposes a smaller number (M) of activattions - typically 1:1 with CPU's
- **Userspace** schedules a larger number (N) of threads onto available activations.
    - Kenel **upcalls** when a thread blocks, returning the activation to userspace.
    - Kernel **upcalls** when a thread wakes up, userspace schedules it on an activation.
    - Kernel controls maximum parallelism by limiting number of activations.
- Threading library is responsible for scheduling user threads on the available schedulable entities; this makes context switching of threads very fast, as it avoids system calls.