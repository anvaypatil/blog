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