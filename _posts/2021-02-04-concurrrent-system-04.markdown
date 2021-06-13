---
layout: post
title: "Concurrent Systems: 04 "
date: 2021-02-04 13:01:20 +0300
description: Concurrency vs Parallism Blocking vs Non-blocking, Lock vs Lock-free # Add post description (optional)
img:  software.jpg # Add image post (optional)(optional)
categories: [concurrent-systems]
icon: blogging.png
---

- **Concurrency** is all about dealing with multiple things at once.
- **Parallelism** is all about doing multiple things at once.

#### Concurrency vs Parallelism
- Concurrency and parallelism are often confused because traditional threads and locks don’t provide any direct support for parallelism.
- If you want to exploit multiple cores, your only choice is to create a concurrent program and then run it on parallel hardware.
- There will always be a need to communicate across parallel or concurrent running tasks. (Tony Hoare Paper)
- The beauty lies in how efficiently you communicate (if need-be) between parallel/concurrent running tasks with lesser waits

#### Parallel Architectures
They exists when we don't need/very less communication between execution
- Bit-Level Parallelism. Why is a 32-bit computer faster than an 8-bit one? Parallelism
- Instruction-Level Parallelism
- Data Parallelism
- Task Level Parallelism


#### Blocking 
When we block one thread waiting for other thread or IO for execution, it is Blocking. ( Thread wait no spin cycle ).
#### Non-Blocking 
When a thread not waiting for execution other thread, it is non-blocking ( With help of Atomic/ CAS supported data structures). Mechanism used in Multi-threaded code
#### Locking 
A way to synchronize / (make two thread's run in sequence)/ Serialize multi-threaded code for task. (With help of Mutex's and semaphore's)
#### Lock-Free 
A way to help multi-threaded code share data/state between themselves. Atomic/ CAS used to create such structures. example: Lock-Free Stack, Queue, Array etc