---
layout: post
title: "Distributed Cache"
date: 2020-12-02 13:01:20 +0300
description: Concepts on Distributed Cache. # Add post description (optional)
img:  system-components.png # Add image post (optional)(optional)
categories: [system-components]
icon: blogging.png
---
 
 - A distributed cache may span multiple servers so that it can grow in size and in transactional capacity. 
 - Mainly used to store application data residing in database and web session data. 
 - Since it has become feasible now because main memory has become very cheap and network cards have become very fast, with 1 Gbit now standard everywhere and 10 Gbit gaining traction. 
 - A distributed cache works well on lower cost machines usually employed for web servers as opposed to database servers which require expensive hardware.

#### Primary uses cases of Distributed Cache
1. **Database Caching**<br/>
The Cache can be placed between Application Server and Database. Where access the data from cache instead of main datastore which frequently accesses data in-memory to cut down latency & unnecessary load on it. There is no DB bottleneck when the cache is implemented.
1. **User Sessions Storing**<br/>
User sessions are mostly stored in the cache to avoid losing the user information in case any of the instances go down.
If any of the instance goes down, a new instance spins up, reads the user data from the cache & continues the session without having the user notice anything amiss.
1. **In-memory Data Lookup**<br/>
If you have a mobile / web app front end you might want to cache some information like user profile, some historical data, or some API response according to your use cases. Caching will help in storing such data.

#### How Distributed cache works in general
1. A Distributed cache under the covers is a Distributed Hash Table which has a responsibility of mapping Object Values to Keys spread across multiple nodes.
1. A hash table manages the addition, deletion, failure of nodes continually as long as the cache service is online. Distributed hash tables were originally used in the peer to peer systems.
1. From design prospective, caches evict data based on the LRU(Least Recently Used policy). Will see the eviction policies in next steps. Basically, it uses a Doubly-Linked-List to manage the data pointers , which is the most important part of the data-structure.

### Some examples of Distributed Cache
- #### Aerospike
    - Modeled under the Shared-nothing architecture and written in C
    - Hybrid memory architecture: the database indices are stored fully in RAM for quick access, while the data is stored on a persistent device using the data layer
    - <a target="_blank" href="https://en.wikipedia.org/wiki/Aerospike_(database)#Features">More ...</a>

- #### Apache Ignite
    - A distributed database for high-performance computing with in-memory speed.
    - based on the shared nothing architecture
    - Utilizes RAM as the default storage and processing tier, thus, belonging to the class of in-memory computing platforms
    - Apache Ignite is a strongly consistent platform that implements two-phase commit protocol
    - Transactions in Apache Ignite are ACID-compliant and can span multiple cluster nodes and caches. 
    - It supports pessimistic and optimistic concurrency modes, deadlock-free transactions and deadlock detection techniques.
    - <a target="_blank" href="https://ignite.apache.org/whatisignite.html">More ...</a> 

- #### Couchbase
    - CouchBase is a combination of Memcached and CouchDB.
    - CouchBase is built on real shared-nothing architecture. That means there is no point of contention, and every node is self-sufficient and independent.
    - Documents get stored in two formats: JSON or Binary, documents get stored in Bucket. Every node has replicated Bucket.
    - Under the hood, these buckets are partitioned into vBuckets. These vBuckets are actually data partitioned.
    - Every cluster maintains a cluster map that maps partition to the server.
    - Every server has a replication factor of 3 for every bucket.
    - Every server maintains a subset of active and replica vBuckets.
    - <a target="_blank" href="https://resources.couchbase.com/c/server-arc-overview">More ...</a> 

- #### Ehcache
    - Ehcache is an open source Java distributed cache for general purpose caching.

- #### Hazelcast
    -  open source in-memory data grid based on Java.
    - Typical use-cases for Hazelcast include:
        -  Application scaling
        -  Cache-as-a-service
        -  Cross-JVM communication and shared storage
        -  Distributed cache, often in front of a database
        -  In-memory processing and Analytics
        -  In-memory computing
        -  Internet of Things infrastructure
        -  Key-value database
        -  Memcached alternative with a protocol compatible interface[6]
        -  Microservices infrastructure
        -  NoSQL data store
        -  Spring Cache
        -  Web Session clustering
    - Vert.x utilizes it for shared storage <a target="_blank" href="https://www.cubrid.org/blog/3826515">[1]</a> 
- #### Infinispan
    -  Java applications can embed it as library pr use it as a service through TCP/IP.
    - Typical use-cases for Infinispan include:
        - Distributed cache, often in front of a database
        - Storage for temporal data, like web sessions
        - In-memory data processing and analytics
        - Cross-JVM communication and shared storage
        - MapReduce Implementation in the In-Memory Data Grid.
    - <a target="_blank" href="https://infinispan.org/docs/stable/titles/overview/overview.html">[more]</a> 
- #### Memcached
    - In-memory key-value store for small chunks of arbitrary data (strings, objects) from results of database calls, API calls, or page rendering HTML.
    - Memcached uses LRU caching algorithm(Least Recently Used (LRU) – discards the least recently used items first).
    - <a target="_blank" href="https://memcached.org/about">[more]</a> 
- #### Oracle Coherence
    - A Java-based distributed cache and in-memory data grid, intended for systems that require high availability, high scalability and low latency, particularly in cases that traditional relational database management systems provide insufficient throughput, or insufficient performance.
    - **Partitioned:** The data in a distributed cache is spread out over all the servers in such a way that no two servers are responsible for the same piece of cached data. The size of the cache and the processing power associated with the management of the cache can grow linearly with the size of the cluster. Also, it means that operations against data in the cache can be accomplished with a "single hop," in other words, involving at most one other server.
    - **Load-Balanced:** Since the data is spread out evenly over the servers, the responsibility for managing the data is automatically load-balanced across the cluster.
    - **Location Transparency:** Although the data is spread out across cluster nodes, the exact same API is used to access the data, and the same behavior is provided by each of the API methods. This is called location transparency, which means that the developer does not have to code based on the topology of the cache, since the API and its behavior is the same with a local JCache, a replicated cache, or a distributed cache.
    - **Failover:** All Coherence services provide failover and failback without any data loss, and that includes the distributed cache service. The distributed cache service allows the number of backups to be configured; if the number of backups is one or higher, any cluster node can fail without the loss of data.
- #### Redis (Remote Dictionary Server))
    - In-memory data structure store, used as a distributed, in-memory key–value database, cache and message broker, with optional durability.
    - Supports different kinds of abstract data structures, such as strings, lists, maps, sets, sorted sets, HyperLogLogs, bitmaps, streams, and spatial indexes
    - Top 5 use cases of Redis
        1. **Session Cache:** Advantages of using Redis over other session stores, such as Memcached, is that Redis offers persistence. While maintaining a cache isn’t typically mission critical with regards to consistency, most users wouldn’t exactly enjoy if all their cart sessions went away, after 1 day, 1 week.
        1. **Full Page Cache (FPC):** Outside of your basic session tokens, Redis provides a very easy FPC platform to operate in. Going back to consistency, even across restarts of Redis instances, with disk persistence your users won’t see a decrease in speed for their page loads.
        1. **Queues:** Taking advantage of Redis’ in memory storage engine to do list and set operations makes it an amazing platform to use for a message queue. Interacting with Redis as a queue should feel native to anyone used to using push/pop operations with lists in programming languages such as Python.
        1. **Leaderboards/Counting:** Redis does an amazing job at increments and decrements since it’s in-memory. Sets and sorted sets also make our lives easier when trying to do these kinds of operations, and Redis just so happens to offer both of these data structures.
        1. **Pub/Sub:** (Like Firebase) An easy way to plug into an event stream, generally between processes or machines. For instance, an user creates a published event. One process handles updating the database from the event, another updates user stats, another global stats, another updates the text search database, etc. They're all loosely coupled by subscribing to the channel. You can add new processes for testing updates and monitoring the system. It's a little different from a message queue in that there's no storing messages until they're processed, but Redis has other structures for those sorts of jobs.
- #### Velocity/AppFabric
    - Provides an in-memory, distributed cache platform for Windows Server.
    - AppFabric Caching stores serialized managed objects in a cache cluster. 
    - The cache cluster consists of one or more machines that pool their available physical memory. 
    - This pooled memory is presented to cache clients as a single source of caching memory. 
    - Objects are stored and accessed using an associated key value.