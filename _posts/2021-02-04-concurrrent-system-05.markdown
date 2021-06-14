---
layout: post
title: "Concurrent Systems: 04 "
date: 2021-02-04 13:01:20 +0300
description: Transactions # Add post description (optional)
img:  software.jpg # Add image post (optional)(optional)
categories: [concurrent-systems]
icon: blogging.png
---
### Transaction
A transaction usually means a sequence of information exchange and related work (such as database updating) that is treated as a unit for the purposes of satisfying a request and for ensuring database integrity.

### Properties of Transactions
- **Atomicity**: A transaction's changes to the state are atomic: either all happen or none happen. These changes include database changes, messages, and actions on transducers.
- **Consistency**: A transaction is a correct transformation of the state. The actions taken as a group do not violate any of the integrity constraints associated with the state.
- **Isolation**: Even though transactions execute concurrently, it appears to each transaction T, that others executed either before T or after T, but not both.
- **Durability**: Once a transaction completes successfully (commits), its changes to the database survive failures and retain its changes.



### Types of Transactions
- **Pessimistic Transactions**  Delay the checking of whether a transaction meets the isolation and other integrity rules (e.g., serializability and recoverability) until its end, without blocking any of its (read, write) operations ("...and be optimistic about the rules being met..."), and then abort a transaction to prevent the violation, if the desired rules are to be violated upon its commit. An aborted transaction is immediately restarted and re-executed, which incurs an obvious overhead (versus executing it to the end only once). If not too many transactions are aborted, then being optimistic is usually a good strategy.
- **Optimistic Transactions** Block an operation of a transaction, if it may cause violation of the rules, until the possibility of violation disappears. Blocking operations is typically involved with performance reduction.
- **Semi-Optimistic Transactions** Block operations in some situations, if they may cause violation of some rules, and do not block in other situations while delaying rules checking (if needed) to transaction's end, as done with optimistic.