---
layout: post
title: "Cache: Basics"
date: 2020-12-01 13:01:20 +0300
description: Impact of cache in system design . # Add post description (optional)
img:  system-components.png # Add image post (optional)(optional)
categories: [system-components]
icon: blogging.png
---
 **Cache** is a temporary storage area where frequently accessed data can be stored for rapid access. Cached data is stored in the memory. Defining frequently accessed data is a matter of judgment and engineering. 
 
 We have to answer two fundamental questions in order to define a solid caching strategy.
 - What resource should be stored in the cache? 
 - How long should the resource be stored in the cache? 

<br/>

### What resource should be stored in the cache? 
#### The locality principle
 This principle came out of work done on the Atlas System’s virtual memory in 1959 <a href="http://denninginstitute.com/pjd/PUBS/CACMcols/cacmJul05.pdf" target="blank">[1]</a>, which provides good guidance on defining temporal and spatial locality. 
 - Temporal locality is based on accessing repeatedly, referenced resources. 
 - Spatial locality states that the data adjacent to recently referenced data will be requested in the near future.

#### Temporal cache
 Temporal locality is well suited for frequently accessed, relatively nonvolatile data — for **example, a drop-down list** on a Web page. The data for the **drop down list can be stored in the cache** at the start of the application on the Web server. For subsequent Web page requests, the drop down list will be populated from the Web server cache and not from the database. This will **save unnecessary database calls and will improve application performance.**

####  Spatial Cache
Consider an **example of tabular data display** like a GridView on UI. Implementing efficient paging on such controls requires complex logic. The logic is based on the number of records displayed per page and the total number of matching records in the underlying database table. We can either perform in-memory paging or hit the database every time the user moves to a different page; both are extreme scenarios. A third solution is to exploit the principle of spatial locality to implement an efficient paging solution. For example, consider a GridView displaying 10 records per page. For 93 records, we will have 10 pages. **Instead of fetching all records in the memory, we can use the spatial cache to optimize this process**. A sliding window algorithm can be used to implement the paging. Let’s define the data window just wide enough to cover most of the user requests, say 30 records. On page one, **we will fetch and cache the first 30 records**. This cache entry can be user session specific or applicable across the application. As a user browses to the third page, the cache will be updated by replacing records in the range of 1–10 by 31–40. **In reality, most users won’t browse beyond the first few pages**. The cache will be discarded after five minutes of inactivity, eliminating the possibility of a memory leak. The logic is based on the spatial dependencies in the underlying dataset. This caching strategy works like a charm on a rarely changing static dataset.

 > Similar strategy is used by sites who show real-time feeds example Twitter, Facebook etc.

 The **drawback** of this logic is the **possibility of a stale cache**. A stale cache is a result of the application modifying the underlying dataset without refreshing the associated cache, producing inconsistent results.
 **To mitigate** this we **use** cache <a target="_blank" href="{{ site.baseurl }}/system-components/cache-write-policies/">write policies</a> to make sure we are always in consistent state.


 <br/>

###  How long should the resource be stored in the cache? 
An important factor in determining an effective caching strategy is the **lifetime of the cached resource**. 
- Resources stored in the temporal cache are good for the life of an application. 
- Resources that are stored in the spatial cache are either time-dependent or place-dependent. 
    - Time-dependent resources should be purged as per the cache expiration policy. 
    - Place-specific resources can be discarded based on the state of the application. 

<br/>
In order to store a new resource in the cache, an existing cached resource will be moved out of the cache to a secondary storage, such as the hard disk. This process is known as paging. This movement of data can be done with various strategies covered under <a target="_blank" href="https://en.wikipedia.org/wiki/Cache_replacement_policies">cache replacement algorithms</a>

## Commanly used Cache Eviction Policies
- **First In First Out (FIFO):** The cache evicts the first block accessed first without any regard to how often or how many times it was accessed before.
- **Last In First Out (LIFO):** The cache evicts the block accessed most recently first without any regard to how often or how many times it was accessed before.
- **Least Recently Used (LRU):** Discards the least recently used items first.
- **Most Recently Used (MRU):** Discards, in contrast to LRU, the most recently used items first.
- **Least Frequently Used (LFU):** Counts how often an item is needed. Those that are used least often are discarded first.